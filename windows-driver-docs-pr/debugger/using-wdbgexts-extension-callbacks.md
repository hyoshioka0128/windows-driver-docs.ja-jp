---
title: WdbgExts 拡張機能コールバックの使用
description: WdbgExts 拡張機能コールバックの使用
ms.assetid: b9a2f30a-b09c-43eb-b105-a6b0ffdb1342
keywords:
- WdbgExts 拡張機能、コールバック、使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 265ba5aa236fa1571337295c1d3accc7ef783806
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838799"
---
# <a name="using-wdbgexts-extension-callbacks"></a>WdbgExts 拡張機能コールバックの使用


## <span id="ddk_using_wdbgexts_extension_callbacks_dbwx"></span><span id="DDK_USING_WDBGEXTS_EXTENSION_CALLBACKS_DBWX"></span>


WdbgExts 拡張 DLL を記述するときに、特定の関数をエクスポートできます。

-   [*Windbgextensiondllinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_extension_dll_init)という名前の関数をエクスポートする必要があります。 デバッガーによって拡張 DLL が読み込まれると、まず*Windbgextensiondllinit*が呼び出され、3つの引数が渡されます。

    -   APIS64 構造体 **\_の WINDBG\_EXTENSION**へのポインター。デバッガーによって実装され、Wdbgexts で宣言されている関数へのポインターが含まれています。 DLL 内に作成するグローバル変数に構造全体をコピーする必要があります。
    -   メジャーバージョン番号。 メジャーバージョン番号は、DLL で作成したグローバル変数にコピーする必要があります。
    -   マイナーバージョン番号。 マイナーバージョン番号は、DLL で作成したグローバル変数にコピーする必要があります。

    たとえば、次の例に示すように、ExtensionApis、SavedMajorVersion、および SavedMinorVersion という名前のグローバル変数を作成できます。

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

-   [*ExtensionApiVersion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_extension_api_version)という名前の関数をエクスポートする必要があります。 デバッガーはこの関数を呼び出し、拡張 DLL のバージョン番号を含む**EXT\_API\_バージョン**構造へのポインターを返します。 デバッガーは、拡張機能のバージョン番号を表示するチェーンや[**バージョン**](version--show-debugger-version-.md)などのコマンド[**を**](-chain--list-debugger-extensions-.md)実行するときに、このバージョン番号を使用します。

-   必要に応じて、 [*Checkversion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_check_version)という名前の関数をエクスポートできます。 デバッガーは、拡張コマンドを使用するたびにこのルーチンを呼び出します。 これを使用すると、DLL のバージョンがデバッガーと少し異なる場合にバージョンの不一致の警告を出力できますが、実行できないようにするための十分な違いはありません。

 

 





