---
title: WdbgExts 拡張機能コールバックを使用します。
description: WdbgExts 拡張機能コールバックを使用します。
ms.assetid: b9a2f30a-b09c-43eb-b105-a6b0ffdb1342
keywords:
- コールバック関数を使用して、WdbgExts 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d58272bc50854d1b0e9f2fa11012cfbdbd68027
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527800"
---
# <a name="using-wdbgexts-extension-callbacks"></a>WdbgExts 拡張機能コールバックを使用します。


## <span id="ddk_using_wdbgexts_extension_callbacks_dbwx"></span><span id="DDK_USING_WDBGEXTS_EXTENSION_CALLBACKS_DBWX"></span>


WdbgExts 拡張 DLL を記述するときに、特定の関数をエクスポートできます。

-   という名前の関数をエクスポートする必要があります[ *WinDbgExtensionDllInit*](https://msdn.microsoft.com/library/windows/hardware/ff561303)します。 最初に呼び出し、デバッガーでは、拡張 DLL が読み込まれたら、 *WinDbgExtensionDllInit*を 3 つの引数を渡します。

    -   ポインターを**WINDBG\_拡張子\_APIS64**構造体は、デバッガーによって実装され、Wdbgexts.h で宣言される関数へのポインターが含まれています。 DLL で作成したグローバル変数に、構造全体をコピーする必要があります。
    -   メジャー バージョン番号。 メジャー バージョン番号は、DLL で作成したグローバル変数にコピーする必要があります。
    -   マイナー バージョン番号。 マイナー バージョン番号は、DLL で作成したグローバル変数にコピーする必要があります。

    たとえば、ExtensionApis、SavedMajorVersion、および次の例に示すように SavedMinorVersion という名前のグローバル変数を作成できます。

    ```cpp
    WINDBG_EXTENSION_APIS64 ExtensionApis;
    USHORT SavedMajorVersion;
    USHORT SavedMinorVersion;

    VOID WinDbgExtensionDllInit(PWINDBG_EXTENSION_APIS64 lpExtensionApis,
        USHORT MajorVersion, USHORT MinorVersion)
    {
       ExtensionApis = *lpExtensionApis;
       SavedMajorVersion = MajorVersion;
       SavedMinorVersion = MinorVersion;
        ...
    }
    ```

-   呼び出される関数をエクスポートする必要があります[ *ExtensionApiVersion*](https://msdn.microsoft.com/library/windows/hardware/ff543968)します。 デバッガーは、この関数を呼び出すし、戻りポインターを要求する**EXT\_API\_バージョン**拡張 DLL のバージョン番号を含む構造体。 などのコマンドを実行するときに、デバッガーはこのバージョン番号を使用して[ **.chain** ](-chain--list-debugger-extensions-.md)と[**バージョン**](version--show-debugger-version-.md)拡張機能のバージョンを表示します。数です。

-   呼び出される関数をエクスポートすることができます必要に応じて[ *CheckVersion*](https://msdn.microsoft.com/library/windows/hardware/ff539096)します。 デバッガーは、拡張機能コマンドを使用するたびに、このルーチンを呼び出します。 これを使用するには、DLL を実行するを防ぐために若干異なるバージョンのデバッガーよりも十分な異なるがない場合は、バージョンの不一致の警告を印刷します。

 

 





