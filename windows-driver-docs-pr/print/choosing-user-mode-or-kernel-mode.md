---
title: ユーザー モードまたはカーネル モードを選択する
description: ユーザー モードまたはカーネル モードを選択する
ms.assetid: 1e63d01e-8cf2-488a-89e8-d4a3ff5cfe19
keywords:
- プリンター グラフィックス DLL WDK、ユーザー モードとカーネル モード
- DLL の WDK プリンター、ユーザー モードとカーネル モードのグラフィックス
- ユーザー モードで WDK プリンター グラフィックスの実行
- カーネル モード実行 WDK プリンター グラフィックス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7effd5c2c5439c27525f03bf9bf0205df242c2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351972"
---
# <a name="choosing-user-mode-or-kernel-mode"></a>ユーザー モードまたはカーネル モードを選択する





プリンター グラフィックス Dll の実行をユーザー モードでは、カーネル モードでの実行に対して次のメリットを提供します。

-   無制限のスタック領域。

-   Win32 Api にアクセスします。

-   システムを発生させる可能性が低いがクラッシュします。

-   デバッグの簡略化、ユーザー モード デバッガーを使用します。

-   浮動小数点の機能、グラフィックス DDI 浮動小数点関数の使用は必須ではないためです。

-   説明されている Microsoft Windows 2000 およびそれ以降のプリンター ドライバーのアーキテクチャの一部ではない、ベンダーから提供されたカスタマイズされたユーザー モード Dll を呼び出す機能

Windows Vista では、カーネル モード プリンター ドライバーをインストールすることはできません。 アプリケーションが行うしようとすると、(Windows SDK のドキュメントで説明) AddPrinterDriver および AddprinterDriverEx 関数はエラー コードのエラーで失敗\_KM\_ドライバー\_ブロックします。

次の表では、許可されているプリンター ドライバーの実行モードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>オペレーティング システムのバージョン</th>
<th>プリンター グラフィックス DLL の実行モードを許可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows NT 4.0</p></td>
<td><p>kernel</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>ユーザーまたはカーネル</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP および Server 2003</p></td>
<td><p>既存のプリンターの使用可能なカーネル モード新しいプリンターのインストールに必要なユーザー モード</p></td>
</tr>
<tr class="even">
<td>Windows Vista</td>
<td><p>ユーザー</p></td>
</tr>
</tbody>
</table>

 

### <a name="using-the-graphics-ddi-in-user-mode"></a>ユーザー モードでのグラフィックス DDI の使用

ユーザー モードのプリンター グラフィックス DLL は呼び出し元に限定されない、 [GDI サポート サービス](https://msdn.microsoft.com/library/windows/hardware/ff566714)への Eng プレフィックス付きのグラフィックス DDI コールバック関数。 ただし、これには従う必要があるいくつかのルールがあります。

-   カーネル モードのようなグラフィックスの Dll、ユーザー モードのグラフィックスの Dll が作成または描画サーフェイスを変更するグラフィックス Ddi を呼び出す必要があります。 これらのコールバック関数は、GDI サポート サービスと、これらの描画関数の Win32 関数を呼び出すことは許可されていません。

    ユーザー モード dll の場合は、これらの描画のコールバック関数への呼び出しは、GDI のカーネル モードのグラフィックス レンダリング エンジン (GRE) への呼び出しを通過し、ユーザー モード GDI クライアントによって受け取られます。

-   Eng プレフィックス付きグラフィックス DDI 関数の次の一覧は、ユーザー モード Dll によって呼び出すことができません。

    [**EngCreatePath**](https://msdn.microsoft.com/library/windows/hardware/ff564755)

    [**EngGetType1FontList**](https://msdn.microsoft.com/library/windows/hardware/ff564956)

    [**EngMapModule**](https://msdn.microsoft.com/library/windows/hardware/ff564974)

    [**EngDebugBreak**](https://msdn.microsoft.com/library/windows/hardware/ff564773)

-   ユーザー モード プリンター グラフィックスの Dll を引き続き使用できますグラフィックス DDI 関数[GDI 浮動小数点サービス](https://msdn.microsoft.com/library/windows/hardware/ff566535)します。

### <a name="converting-an-existing-printer-graphics-dll-to-user-mode"></a>プリンター グラフィックス DLL をユーザー モードに変換します。

以前プリンター グラフィックス カーネル モードで実行される DLL を開発した場合は、ユーザー モードでの実行に、DLL を変換できます。 変換すると、単に追加、 [ **DrvQueryDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556261) DLL に関数を次の規則に従う[プリンター グラフィックス DLL をビルド](building-a-printer-graphics-dll.md)します。

### <a name="creating-a-new-printer-graphics-dll-in-user-mode"></a>ユーザー モードでの新しいプリンター グラフィックス DLL の作成

新しいプリンター グラフィックス ユーザー モードで実行する DLL を開発するには、カーネル モード Dll によって使用されるすべてのグラフィックス DDI 関数を使用して続行することができます。 ただし、次のオプションもあります。

-   持つの正確な Win32 関数への Eng プレフィックス付きの関数では、Win32 関数を呼び出すことを強くお勧めします。 次の表では、これらへの Eng プレフィックス付きの関数は、対応する Win32 と共に一覧表示します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng プレフィックス付きの関数</th>
    <th>Win32 と同等</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>EngAllocMem</p></td>
    <td><p>HeapAlloc</p></td>
    </tr>
    <tr class="even">
    <td><p>EngAllocUserMem</p></td>
    <td><p>HeapAlloc</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngEnumForms</p></td>
    <td><p>EnumForms</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFreeMem</p></td>
    <td><p>選択肢</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngFreeUserMem</p></td>
    <td><p>選択肢</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFindImageProcAddress</p></td>
    <td><p>GetProcAddress</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetForm</p></td>
    <td><p>GetForm</p></td>
    </tr>
    <tr class="even">
    <td><p>EngGetLastError</p></td>
    <td><p>最新エラーの取得</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetPrinter</p></td>
    <td><p>GetPrinter</p></td>
    </tr>
    <tr class="even">
    <td><p>EngGetPrinterData</p></td>
    <td><p>GetPrinterData</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetPrinterDriver</p></td>
    <td><p>GetPrinterDriver</p></td>
    </tr>
    <tr class="even">
    <td><p>EngLoadImage</p></td>
    <td><p>LoadLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngMulDiv</p></td>
    <td><p>MulDiv</p></td>
    </tr>
    <tr class="even">
    <td><p>EngSetLastError</p></td>
    <td><p>SetLastError</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngSetPrinterData</p></td>
    <td><p>SetPrinterData</p></td>
    </tr>
    <tr class="even">
    <td><p>EngUnloadImage</p></td>
    <td><p>FreeLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngWritePrinter</p></td>
    <td><p>WritePrinter</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   同様の機能での Win32 関数に対応するへの Eng プレフィックス付きの関数で Win32 関数を呼び出すことを強くお勧めします。 次の表では、いくつかの Win32 の対応すると共に、これらへの Eng プレフィックス付き関数の一覧表示します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng プレフィックス付きの関数</th>
    <th>Win32 と同等</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>EngAcquireSemaphore</p></td>
    <td><p>EnterCriticalSection</p></td>
    </tr>
    <tr class="even">
    <td><p>EngCreateSemaphore</p></td>
    <td><p>CRITICAL_SECTION オブジェクトを割り当て、Win32 InitializeCriticalSection 関数の呼び出しを使用して初期化します。</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngDeleteSemaphore</p></td>
    <td><p>DeleteCriticalSection</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFindResource</p></td>
    <td><p>FindResource</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngFreeModule</p></td>
    <td><p>FreeLibrary</p></td>
    </tr>
    <tr class="even">
    <td><p>EngLoadModule</p></td>
    <td><p>LoadLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngMultiByteToWideChar</p></td>
    <td><p>MultiByteToWideChar</p></td>
    </tr>
    <tr class="even">
    <td><p>EngQueryLocalTime</p></td>
    <td><p>GetLocalTime</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngReleaseSemaphore</p></td>
    <td><p>ReleaseSemaphore</p></td>
    </tr>
    <tr class="even">
    <td><p>EngWideCharToMultiByte</p></td>
    <td><p>WideCharToMultiByte</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   関数の作成または描画サービスを変更する場合、新しいドライバーが呼び出しを続ける必要があります[GDI サポート サービス](https://msdn.microsoft.com/library/windows/hardware/ff566714)と、Win32 関数ではありません。

-   グラフィックスを使用する代わりに DDI 関数の[GDI 浮動小数点サービス](https://msdn.microsoft.com/library/windows/hardware/ff566535)、FLOAT データ型を使用することができます。

 

 




