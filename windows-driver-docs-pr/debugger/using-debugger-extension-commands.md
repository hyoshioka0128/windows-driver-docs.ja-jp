---
title: デバッガー拡張機能コマンドの使用
description: デバッガー拡張機能コマンドの使用
ms.assetid: 1db9a835-accb-41b9-9ab1-c4c9f0596aa5
keywords:
- 拡張コマンド (コマンド)、使用
- 拡張コマンド (コマンド)、既定の検索順序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 422998f608ed896d9efb7096f874836ab5eed69b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209674"
---
# <a name="using-debugger-extension-commands"></a>デバッガー拡張機能コマンドの使用


## <span id="ddk_using_debugger_extension_commands_dbg"></span><span id="DDK_USING_DEBUGGER_EXTENSION_COMMANDS_DBG"></span>


デバッガーの拡張コマンドの使用は、[デバッガーコマンド](using-debugger-commands.md)を使用する場合とよく似ています。 このコマンドはデバッガーコマンドウィンドウに入力され、このウィンドウに出力するか、ターゲットアプリケーションまたはターゲットコンピューターの変更を生成します。

実際のデバッガー拡張機能コマンドは、デバッガーによって呼び出される DLL 内のエントリポイントです。

デバッガーの拡張機能は、次の構文で呼び出されます。

**!\[** <em>module</em>**.\]**<em>拡張機能</em> **\[**<em>引数</em>**\]**

モジュール名の後に .dll ファイル名拡張子を指定することはできません。 *モジュール*に完全なパスが含まれている場合、既定の文字列サイズの制限は255文字です。

モジュールがまだ読み込まれていない場合は、 **LoadLibrary**(*module*) の呼び出しを使用してデバッガーに読み込まれます。 デバッガーによって拡張ライブラリが読み込まれると、 **GetProcAddress**関数が呼び出され、拡張モジュールの拡張機能名が検索されます。 拡張機能名は大文字と小文字が区別され、拡張モジュールの .def ファイルに表示されるとおりに入力する必要があります。 拡張機能のアドレスが見つかった場合は、拡張機能が呼び出されます。

### <a name="span-idsearch_orderspanspan-idsearch_orderspansearch-order"></a><span id="search_order"></span><span id="SEARCH_ORDER"></span>検索順序

モジュール名が指定されていない場合、このエクスポートのために読み込まれた拡張モジュールがデバッガーによって検索されます。

既定の検索順序は次のとおりです。

1.  すべてのオペレーティングシステムと、両方のモードで動作する拡張モジュール: Dbghelp .dll と winext\\ext。

2.  すべてのモードで動作し、オペレーティングシステム固有の拡張モジュール。 Windows XP 以降のバージョンの Windows では、これは winxp\\exts .dll です。 

3.  拡張モジュールは、すべてのオペレーティングシステムで動作しますが、モード固有です。 カーネルモードの場合、これは winext\\kext .dll です。 ユーザーモードの場合、これは winext\\uext です。

4.  オペレーティングシステム固有であり、モード固有の拡張モジュール。 次の表は、このモジュールを示しています。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">ユーザーモード</th>
    <th align="left">カーネルモード</th>
    </tr>
    </thead>
    <tbody>
    <tr class="even">
    <td align="left"><p>winxp \ ntsdexts .dll</p></td>
    <td align="left"><p>winxp の .dll</p></td>
    </tr>
    </tbody>
    </table>

     

拡張モジュールがアンロードされると、その拡張モジュールは検索チェーンから削除されます。 拡張モジュールが読み込まれると、検索順序の先頭に追加されます。 [**Setdll (既定の拡張 DLL の設定)**](-setdll--set-default-extension-dll-.md)コマンドを使用すると、任意のモジュールを検索チェーンの最上位に昇格させることができます。 このコマンドを繰り返し使用すると、検索チェーンを完全に制御できます。

[**チェーン (デバッガー拡張機能の一覧)**](-chain--list-debugger-extensions-.md)コマンドを使用して、読み込まれているすべての拡張モジュールの一覧を現在の検索順序で表示します。

読み込まれている拡張モジュールに含まれていない拡張コマンドを実行しようとすると、"エクスポートが見つかりません" というエラーメッセージが表示されます。

 

 





