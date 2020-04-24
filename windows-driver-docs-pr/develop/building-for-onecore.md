---
ms.assetid: ee46801a-4fa5-465a-aa81-5e76eb83d315
title: OneCore をターゲットとしたビルド
description: 1 つのバイナリのビルドで、Windows 10 以前のエディションと OneCore エディションをターゲットとすることができます。
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0aefa62ad1fbf120ffb6b905c9aafbdb5b44f5ab
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63382491"
---
# <a name="building-for-onecore"></a>OneCore をターゲットとしたビルド

Visual Studio を使用して Windows 10 のユーザーモード コードをビルドするときに、特定のバージョンの Windows をターゲットとするようにリンカー オプションをカスタマイズできます。  次の要因について検討します。

* ビルドしたバイナリは、Windows の最新バージョンのみで実行されますか?  それとも、以前のバージョン (Windows 7 など) でも実行できますか。  

* プロジェクトは、[UWP](https://docs.microsoft.com/windows/uwp/get-started/whats-a-uwp) と依存関係がありますか?

たとえば、新しい UMDF v2 ドライバー プロジェクトを作成した場合、Visual Studio は既定で `OneCoreUAP.lib` にリンクします。  これにより、最新バージョンの Windows で動作し、UWP 機能を追加できるバイナリが作成されます。

ただし、要件によっては、代わりに `OneCore.lib` をリンクすることができます。 次の表は、各ライブラリに対応するシナリオを示したものです。

|ライブラリ|シナリオ|
|-|-|
|`OneCore.lib`|Windows 7 以降のすべてのエディション (UWP のサポートなし)|
|`OneCoreUAP.lib`|Windows 7 以降、Windows 10 の UWP エディション (デスクトップ、IoT、HoloLens。ただし、Nano Server を除く)|

>[!NOTE]
>Visual Studio でリンカー オプションを変更するには、プロジェクトのプロパティを選択して、 **[リンカー] -> [入力] -> [追加の依存ファイル]** に移動します。

Windows API のサブセットは正常にコンパイルされますが、デスクトップ以外の OneCore エディション (モバイルや IoT など) ではランタイム エラーが返されます。

たとえば、[**InstallApplication**](https://docs.microsoft.com/windows/desktop/api/appmgmt/nf-appmgmt-installapplication) 関数は、デスクトップ以外の OneCore エディションで `ERROR_ NOT_SUPPORTED` を返します。  これらの問題は [ApiValidator](validating-universal-drivers.md)ツールでも報告されます。 次のセクションでは、この問題を修正する方法について説明します。

## <a name="fixing-apivalidator-errors-by-using-isapisetimplemented"></a>[**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) を使用して ApiValidator のエラーを修正する

コードで非ユニバーサル API を呼び出すと、次の [ApiValidator](validating-universal-drivers.md) エラーが返される場合があります。

* `Error: <Binary Name> has unsupported API call to <Module Name><Api Name>`
    
    アプリやベース ドライバーを Windows 10 と以前のバージョンの Windows で実行する必要がある場合は、上記のカテゴリの API 呼び出しを削除する必要があります。

* `Error: <Binary Name> has a dependency on <Module Name><Api Name> but is missing: IsApiSetImplemented("<contract-name-for-Module>)`
    
    上記のカテゴリの API 呼び出しは正常にコンパイルされますが、対象のオペレーティング システムによっては、実行時に想定どおりの動作をしない可能性があります。 [DCHU](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers#design-principles) の U の要件に適合させるには、これらの呼び出しを [**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) でラップします。

これにより、コードをエラーなくコンパイルすることができます。  その後の実行時に、ターゲット コンピューターに必要な API がない場合は、[**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) で FALSE が返されます。

次のコード サンプルは、これを行う方法を説明したものです。

## <a name="code-sample-direct-usage-of-api-without-evaluating-for-existence"></a>コード サンプル:API の有無を評価せずに API を直接使用する

このコードは、Windows 10 より前のバージョンの Windows では正しく動作しますが、Windows 10 の OneCore エディションで実行すると、WTSEnumerateSessions エラー :78 または ERROR_CALL_NOT_IMPLEMENTED 120 (0x78) が返されます。

このコード サンプルは DCHU の U 部分に適合していないため、実行すると [ApiValidator](validating-universal-drivers.md) エラーが返されます。

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```
コードは次のようになります。

```cpp
#include <windows.h>
#include <stdio.h>
#include <Wtsapi32.h>

int __cdecl wmain(int /* argc */, PCWSTR /* argv */ [])
{
    PWTS_SESSION_INFO pInfo = {};
    DWORD count = 0;

    if (WTSEnumerateSessionsW(WTS_CURRENT_SERVER_HANDLE, 0, 1, &pInfo, &count))
    {
        wprintf(L"SessionCount = %d\n", count);

        for (ULONG i = 0; i < count; i++)
        {
            PWTS_SESSION_INFO pCurInfo = &pInfo[i];
            wprintf(L"    %s: ID = %d, state = %d\n", pCurInfo->pWinStationName, pCurInfo->SessionId, pCurInfo->State);
        }

        WTSFreeMemory(pInfo);
    }
    else
    {
        wprintf(L"WTSEnumerateSessions failure : %x\n", GetLastError());
    } 

    return 0;
}
```

## <a name="code-sample-direct-usage-of-api-after-evaluating-for-existence"></a>コード サンプル:API の有無を評価した後に API を直接使用する

このサンプルは、[**IsApiSetImplemented**](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented) を呼び出す方法を示したものです。 このサンプルは DCHU の U 部分に適合しており、実行すると次の [ApiValidator](validating-universal-drivers.md) 出力が返されます。

```cpp
ApiValidation: All binaries are Universal
```

コードは次のようになります。

```cpp
#include <windows.h>
#include <stdio.h>
#include <Wtsapi32.h>

int __cdecl wmain(int /* argc */, PCWSTR /* argv */ [])
{
    PWTS_SESSION_INFO pInfo = {};
    DWORD count = 0;

    if (!IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0"))
    {
        wprintf(L"IsApiSetImplemented on ext-ms-win-session-wtsapi32-l1-1-0 returns FALSE\n");
    }
    else
    {
        if (WTSEnumerateSessionsW(WTS_CURRENT_SERVER_HANDLE, 0, 1, &pInfo, &count))
        {
            wprintf(L"SessionCount = %d\n", count);

            for (ULONG i = 0; i < count; i++)
            {
                PWTS_SESSION_INFO pCurInfo = &pInfo[i];
                wprintf(L"    %s: ID = %d, state = %d\n", pCurInfo->pWinStationName, pCurInfo->SessionId, pCurInfo->State);
            }

            WTSFreeMemory(pInfo);
        }
        else
        {
            wprintf(L"WTSEnumerateSessions failure : %x\n", GetLastError());
        }
    }

    return 0;
}
```

## <a name="recommended-actions"></a>推奨される操作

* 上記のリンカー オプションを確認し、それに応じて、Visual Studio プロジェクトを更新します。
* WDK の [ApiValidator](validating-universal-drivers.md) ツールを使います。  このツールは、Visual Studio でのドライバーのビルド時に自動的に実行されます。
* 実行時テストを使って、デスクトップ以外の OneCore のエディションで、想定どおりにユーザーモード コードが実行されていることを確認します。  スタブ API が別のエラー コードを生成する場合があることに注意してください。

## <a name="see-also"></a>参照

* [ユニバーサル Windows ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/develop/validating-universal-drivers)
* [OneCore](https://docs.microsoft.com/windows-hardware/get-started/what-s-new-in-windows)

<!--API BOILERPLATE: Compiles using OneCore.lib but returns ERROR_CALL_NOT_IMPLEMENTED on non-Desktop OneCore editions.-->
