---
title: 進行中のインストールの確認
description: 進行中のインストールの確認
ms.assetid: 9630a22e-65df-41f1-bfaf-ef4df9ca8aed
keywords:
- 進行状況の WDK のインストール
- チェックの実行中のインストール
- 実行中のインストール状態の検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2da342604306c7a3123d45ca61555d97809d6a9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357986"
---
# <a name="checking-for-in-progress-installations"></a>進行中のインストールの確認

*デバイス インストール アプリケーション*そのインストールを実行する前に他のインストール操作が進行中ですがかどうかを判断する必要があります。 この判断をするためには、デバイスのインストール アプリケーションを呼び出す必要があります[ **CMP_WaitNoPendingInstallEvents**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_waitnopendinginstallevents)、ゼロのタイムアウト値を通常します。 インストール操作が保留中でこの関数の戻り値では、その他のことを示す場合 (たとえば、新しい Found ハードウェア ウィザードは、アクティブな可能性があります)、デバイスのインストール アプリケーションを終了する必要があります。

させる、*デバイス インストール アプリケーション*をサポートしないプラットフォームと互換性のある**CMP_WaitNoPendingInstallEvents**アプリケーションは、次のコードを含める必要があります。

```cpp
BOOL
IsDeviceInstallInProgress (VOID)
{
    HMODULE hModule;
    CMP_WAITNOPENDINGINSTALLEVENTS_PROC pCMP_WaitNoPendingInstallEvents;

    hModule = GetModuleHandle(TEXT("setupapi.dll"));
    if(!hModule)
    {
        // Should never happen since we're linked to SetupAPI, but...
        return FALSE;
    }

    pCMP_WaitNoPendingInstallEvents =
        (CMP_WAITNOPENDINGINSTALLEVENTS_PROC)GetProcAddress(hModule,
                                             "CMP_WaitNoPendingInstallEvents");
    if(!pCMP_WaitNoPendingInstallEvents)
    {
        // We're running on a release of the operating system that doesn't supply this function.
        // Trust the operating system to suppress AutoRun when appropriate.
        return FALSE;
    }
    return (pCMP_WaitNoPendingInstallEvents(0) == WAIT_TIMEOUT);
}

int
__cdecl
_tmain(IN int argc, IN PTCHAR argv[])
{
    if(IsDeviceInstallInProgress()) {
        //
        // We don't want to start right now.  Instead, our
        // device co-installer will invoke this application
        // (if necessary) during finish-install processing.
        //
        return -1;
    }
    .
    .
}
```

このコードの使用に基づいて、内部設置型の場合に、プラットフォームはサポートしていません**CMP_WaitNoPendingInstallEvents**、インストール操作が進行中である場合に、プラットフォームが自動実行を開始できません。

このコードの使用例、下のトースター インストール パッケージを参照してください、 *src\\全般\\トースター* Windows Driver Kit (WDK) のサブディレクトリ。
