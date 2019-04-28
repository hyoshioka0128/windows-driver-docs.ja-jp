---
title: デバッガー拡張機能コマンドの使用
description: デバッガー拡張機能コマンドの使用
ms.assetid: 1db9a835-accb-41b9-9ab1-c4c9f0596aa5
keywords:
- 使用して拡張機能コマンド (コマンド)
- 拡張機能のコマンド (コマンド)、既定の検索順序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5885e7900d7814f34e77949d64394da4feec5821
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371578"
---
# <a name="using-debugger-extension-commands"></a>デバッガー拡張機能コマンドの使用


## <span id="ddk_using_debugger_extension_commands_dbg"></span><span id="DDK_USING_DEBUGGER_EXTENSION_COMMANDS_DBG"></span>


デバッガーの拡張機能コマンドの使用を使用するとよく似ています[デバッガー コマンド](using-debugger-commands.md)します。 このウィンドウで出力または対象のアプリケーションまたは対象のコンピューターの変更のいずれかの生成のデバッガー コマンド ウィンドウで、コマンドが入力されます。

実際のデバッガーの拡張機能コマンドでは、デバッガーによって呼び出される DLL にエントリ ポイントです。

次の構文では、デバッガーの拡張機能が呼び出されます。

**!\[** <em>モジュール</em>**.\]**<em>拡張子</em> **\[**<em>引数</em>**\]**

モジュール名が .dll ファイル名拡張子を持つ従わないする必要があります。 場合*モジュール*完全なパスを含む既定の文字列のサイズ制限は 255 文字です。

モジュールが読み込まれていない場合、呼び出しに使用して、デバッガーに読み込まれます**LoadLibrary**(*モジュール*)。 デバッガーには、拡張ライブラリが読み込まれますが、後に呼び出して、 **GetProcAddress**拡張モジュール内で拡張機能の名前を検索する関数。 拡張機能名は大文字小文字を区別し、拡張モジュールの .def ファイル内に表示されているとおりに入力する必要があります。 拡張機能のアドレスが見つかった場合、拡張機能が呼び出されます。

### <a name="span-idsearchorderspanspan-idsearchorderspansearch-order"></a><span id="search_order"></span><span id="SEARCH_ORDER"></span>検索順序

モジュール名が指定されていない場合、デバッガーはこのエクスポート用の拡張機能が読み込まれたモジュールを検索します。

既定の検索順序は次のとおりです。

1.  両方のモードですべてのオペレーティング システムで作業する拡張機能モジュール:Dbghelp.dll と winext\\ext.dll します。

2.  すべてのモードで動作するオペレーティング システム固有は、拡張機能モジュール。 Windows XP と Windows の以降のバージョンでは、これは winxp\\exts.dll します。 Windows 2000 の対応するモジュールはありません。

3.  すべてのオペレーティング システムで動作しますが、特定のモードは、拡張機能モジュール。 カーネル モードの場合は、これは winext\\kext.dll します。 ユーザー モードでは、これは winext\\uext.dll します。

4.  オペレーティング システム固有またはモード固有の両方である拡張機能モジュール。 次の表では、このモジュールを指定します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">ユーザー モード</th>
    <th align="left">カーネル モード</th>
    </tr>
    </thead>
    <tbody>
    <tr class="even">
    <td align="left"><p>winxp \ ntsdexts.dll</p></td>
    <td align="left"><p>winxp \ kdexts.dll</p></td>
    </tr>
    </tbody>
    </table>

     

拡張モジュールが読み込まれると、検索のチェーンから削除されます。 拡張モジュールが読み込まれるときに、検索の順序の先頭に追加されます。 [ **.Setdll (既定の拡張 DLL の設定)** ](-setdll--set-default-extension-dll-.md)コマンドは、検索のチェーンの先頭に任意のモジュールの昇格に使用することができます。 このコマンドを繰り返し使用すると、検索のチェーンを完全に制御できます。

使用して、 [ **.chain (リスト デバッガー拡張)** ](-chain--list-debugger-extensions-.md)コマンドを現在の検索順序で読み込まれた拡張機能のすべてのモジュールの一覧を表示します。

拡張機能が読み込まれたモジュールのいずれかではない拡張機能のコマンドを実行しようとすると、エクスポートが見つかりません。 エラー メッセージが表示されます。

 

 





