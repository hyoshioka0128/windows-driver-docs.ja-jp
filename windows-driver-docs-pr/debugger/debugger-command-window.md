---
title: WinDbg でのデバッガー コマンドの入力
description: WinDbg デバッガー コマンド ウィンドウで、デバッガー コマンドを入力します。
ms.assetid: 4d839170-efaf-43d5-a81c-ac3b9c33586c
keywords: debugging information windows, command window, WinDbg
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe50b414433ac31028a55e6ea0ee2c49092c817
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376902"
---
# <a name="entering-debugger-commands-in-windbg"></a>WinDbg でのデバッガー コマンドの入力


## <span id="ddk_debugger_command_window_dbg"></span><span id="DDK_DEBUGGER_COMMAND_WINDOW_DBG"></span>


デバッガー コマンド ウィンドウは、WinDbg で主にデバッグ情報ウィンドウです。 デバッガー コマンドを入力し、このウィンドウで、コマンドの出力を表示できます。

**注**  このウィンドウは、"Command"をタイトル バーが表示されます。 ただし、このドキュメントを常にウィンドウを参照するこの「デバッガー コマンド ウィンドウ」として Microsoft MS-DOS のコマンドを発行するために使用されているコマンド プロンプト ウィンドウで、混乱しないようにします。

 

### <a name="span-idopeningthedebuggercommandwindowspanspan-idopeningthedebuggercommandwindowspanopening-the-debugger-command-window"></a><span id="opening_the_debugger_command_window"></span><span id="OPENING_THE_DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウを開く

デバッガー コマンド ウィンドウを開くには、次のように選択します。**コマンド**から、**ビュー**メニュー。 (ALT + 1 を押すことも をクリックしてまたは、**コマンド**ボタン (![デバッガー コマンド ウィンドウのボタンのスクリーン ショット](images/tbcmd.png)) ツールバー。 ALT + SHIFT + 1 ウィンドウを閉じる、デバッガー コマンドです。)

次のスクリーン ショットでは、デバッガー コマンド ウィンドウの例を示します。

![デバッガー コマンド ウィンドウの例のスクリーン ショット](images/window-command.png)

### <a name="span-idusingthedebuggercommandwindowspanspan-idusingthedebuggercommandwindowspanusing-the-debugger-command-window"></a><span id="using_the_debugger_command_window"></span><span id="USING_THE_DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウの使用

デバッガー コマンド ウィンドウは、2 つのペインに分割されます。 ウィンドウの下部にある小さいウィンドウ (コマンドのエントリのウィンドウ) でのコマンドを入力し、ウィンドウの上部にある大きいウィンドウに出力を表示します。

コマンドのエントリ ウィンドウで ↑ キーおよび ↓ キーを使用して、コマンド履歴をスクロールします。 コマンドが表示されたら、編集または enter キーを押してコマンドを実行できます。

デバッガー コマンド ウィンドウには、その他のコマンドのショートカット メニューが含まれています。 このメニューにアクセスするには、ウィンドウのタイトル バーを右クリックするかウィンドウ (右上隅のアイコンをクリックします。![デバッガー コマンド ウィンドウのツールバーのショートカット メニューにアクセスするためのボタンのスクリーン ショット ](images/tbcmd.png)). 次の一覧では、メニュー コマンドの一部について説明します。

-   **コマンドの出力に追加**のようなコマンドの出力にコメントを追加、[編集 |コマンドの出力に追加](edit---add-to-command-output.md)コマンド。

-   **コマンドの出力をクリア** ウィンドウでテキストをすべて削除します。

-   **テキストの色および色の選択範囲を選択してください.** デバッガー コマンド ウィンドウで選択されているテキストを表示するテキストの色を選択することができます ダイアログ ボックスを開きます。

-   **ワード ラップ**オンとオフは、ワード ラップの状態をオンにします。 このコマンドは、ウィンドウ全体に影響を与える、この状態を選択した後で使用するだけでなくコマンドします。 コマンドと拡張機能の多くは、書式設定された表示を生成するためのワード ラップを使用することにはしないでください。

-   **現在の場所をマーク**コマンド ウィンドウで現在のカーソル位置マーカーを設定します。 マークの名前は、カーソルの右側の行の内容です。

-   **マークに移動して**ウィンドウをスクロールして、選択したマークを含む行がウィンドウの上部に配置されているようにします。

-   **常に浮動**ドッキング場所にドラッグされる場合でも、ドッキングされていない場合、維持するウィンドウが。

-   **フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

 

 





