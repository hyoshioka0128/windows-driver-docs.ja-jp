---
title: デバッガー コマンドを使用します。
description: このセクションでは、デバッガー コマンドを使用して説明します。 ウィンドウの下部にあるプロンプトでコマンドを入力したとします。
ms.assetid: 64dcc364-53b5-41d3-9266-abcfe4b328f4
keywords: コマンド、デバッガー コマンド、メタ コマンド
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77bf91529add011f250f17e483bc37311015597b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537736"
---
# <a name="using-debugger-commands"></a>デバッガー コマンドを使用します。


## <span id="ddk_using_debugger_commands_dbg"></span><span id="DDK_USING_DEBUGGER_COMMANDS_DBG"></span>


KD、CDB は、「デバッガー コマンド ウィンドウ」は、ウィンドウ全体を指します。 ウィンドウの下部にあるプロンプトでコマンドを入力したとします。 コマンドは、任意の出力がある場合、ウィンドウは出力を表示し、もう一度、プロンプトを表示します。

Visual Studio は、「デバッガー コマンド ウィンドウ」はウィンドウのタイトル バーで「デバッガーのイミディ エイト ウィンドウ」と呼びますを参照します。 このウィンドウには、2 つのペインがあります。

-   Small、下部のペインでは、コマンドを入力します。

-   規模が大きく、上部のウィンドウでは、コマンドの出力を表示します。

WinDbg を「デバッガー コマンド ウィンドウ」というラベルの付いた"Command"のタイトル バーで、ウィンドウを指します。 このウィンドウには、2 つのペインが含まれています。

-   Small、下部のペインでは、コマンドを入力します。

-   規模が大きく、上部のウィンドウでは、コマンドの出力を表示します。

このウィンドウは、デバッグ セッションの先頭にはオープンでは常にします。 再び開くか、クリックしてこのウィンドウに切り替えることができます**コマンド**上、**ビュー** ] メニューの [ALT + 1 を押すかをクリックすると、**コマンド (Alt + 1)** ボタン (![スクリーン ショットデバッガー コマンド ウィンドウのボタンの](images/tbcmd.png)) ツールバー。

↑ キーおよび ↓ キーを使用して、コマンド履歴をスクロールすることができます。 前のコマンドが表示されたらは、それを編集し、前のコマンド (または前のコマンドの編集後のバージョン) を実行するには ENTER キーを押します。 カーソルを正常に動作するには、このプロシージャの行の end に存在する必要はありません。

### <a name="span-iddebuggercommandwindowpromptspanspan-iddebuggercommandwindowpromptspandebugger-command-window-prompt"></a><span id="debugger_command_window_prompt"></span><span id="DEBUGGER_COMMAND_WINDOW_PROMPT"></span>デバッガーのウィンドウのコマンド プロンプト

ユーザー モードを実行している場合、デバッグ、デバッガーのコマンド プロンプト ウィンドウはように次の例。

`2:005>`

前の例では、2 は、現在のプロセス数と 005 は現在のスレッド数です。

1 つ以上のコンピューターをデバッガーをアタッチする場合は、次の例のように、プロセスとスレッドの番号の前にシステム番号が含まれています。

`3:2:005>`

この例では、3 は、現在のシステム番号、2 は、現在のプロセス数および 005 は現在のスレッドの数。

カーネル モードの 1 つだけのプロセッサがターゲット コンピューターでのデバッグを実行している場合、プロンプトは、次の例のようになります。

`kd>`

ただし、ターゲット コンピューターに複数のプロセッサがある場合は、次の例のように、プロンプトの前に、現在のプロセッサの数が表示されます。

`0: kd> `

デバッガーが以前に発行されたコマンドの処理でビジー状態の場合は、新しいコマンドは一時的に処理されませんをコマンド バッファーへの追加。 さらに、使用することできますも[コントロール キー](control-keys.md)の KD、CDB、メニュー コマンドを使用して引き続きことができます。 すると、[ショートカット キー](keyboard-shortcuts.md) WinDbg でします。 KD、CDB またはこのビジー状態では、ときに、プロンプトは表示されません。 WinDbg は、このビジー状態では、次のインジケーターは、プロンプトの代わりに表示されます。

`*BUSY* `

使用することができます、 [ **.pcmd (プロンプトの Set コマンド)** ](-pcmd--set-prompt-command-.md)このプロンプトにテキストを追加するコマンド。

### <a name="span-idkindsofcommandsspanspan-idkindsofcommandsspankinds-of-commands"></a><span id="kinds_of_commands"></span><span id="KINDS_OF_COMMANDS"></span>コマンドの種類

WinDbg、KD、CDB、さまざまなコマンドをサポートします。 いくつかのコマンドは、デバッガーの間で共有され、いくつか 1 つまたは 2 つのデバッガーでのみ使用できます。

いくつかのコマンドは、ライブ デバッグでのみ使用できますし、その他のコマンドは、ダンプ ファイルをデバッグする場合にのみ使用します。

いくつかのコマンドは、ユーザー モードのデバッグ中にのみ使用し、その他のコマンドは、カーネル モードのデバッグ中にのみ使用します。

いくつかのコマンドは、特定のプロセッサで、ターゲットが実行されている場合にのみ使用できます。 すべてのコマンドとその制限に関する詳細については、[デバッガー コマンド](debugger-commands.md)を参照してください。

### <a name="span-ideditingrepeatingandcancelingcommandsspanspan-ideditingrepeatingandcancelingcommandsspanediting-repeating-and-canceling-commands"></a><span id="editing__repeating__and_canceling_commands"></span><span id="EDITING__REPEATING__AND_CANCELING_COMMANDS"></span>編集、繰り返し、およびコマンドのキャンセル

コマンドを入力するときに、標準の編集キーを使用できます。

-   ↑ キーおよび ↓ キーを使用して、前のコマンドを検索します。

-   バック スペース、DELETE、INSERT、および左矢印および右矢印キーを使用して、現在のコマンドを編集します。

-   現在の行をオフに ESC キーを押します。

テキスト エントリを自動的に完了するタブ キーを押すことができます。 デバッガーのようなには、コマンドを自動的に完了するには少なくとも 1 つの文字を入力した後、TAB キーを押します。 順番にテキストの入力候補オプション、および SHIFT キーを押しながら TAB キーを押しますに繰り返し TAB キーを押します。 テキストのワイルドカード文字を使用し、tab キーを押してテキストの入力候補オプションの完全なセットを展開できます。 たとえば、入力した**fo\*! ba**とし、TAB キーを押して、デバッガーがモジュールの名前が"fo"で始まるすべてのモジュールで"ba"で始まるすべての記号のセットに展開されます。 」と入力して、それらの"prcb"を持つすべての拡張機能コマンドを完了する別の例として **!\*prcb**し、TAB キーを押すとします。

テキスト補完を実行する、テキスト フラグメントは、ピリオド (.) で始まる場合、TAB キーを使用すると、テキストはドット コマンドに一致します。 テキスト フラグメントは、感嘆符 (!) で始まっている場合は、拡張機能のコマンド テキストが一致します。 それ以外の場合、テキストは、シンボルと一致します。 ときにする機能を使用、TAB キー、TAB キーを押すと、シンボルを入力するコードと種類のシンボル名とモジュール名を完了します。 明らかなモジュール名がない場合は、ローカル シンボルとモジュール名が行います。 モジュールまたはモジュール パターンを指定すると、シンボルの完了は、すべての一致項目からのコードと種類のシンボルを完了します。

自動的にクリップボードの内容を入力しているコマンドに貼り付けるデバッガー コマンド ウィンドウで右クリックすることができます。

コマンドの最大長は、4096 文字です。 ただし場合、[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)行の最大長は 512 文字です。

CDB および KD には、ENTER キーを押して自体と、前のコマンドを繰り返します。 、WinDbg では、有効または、この動作を無効にできます。 この動作の詳細については、[ **」と入力 (最後のコマンドを繰り返します)**](enter--repeat-last-command-.md)を参照してください。

発行した最後のコマンドは、長い表示を表示します。 カットが、使用する場合、 [ **CTRL + C** ](ctrl-c--break-.md) KD、CDB、またはキー。 WinDbg を使用して[デバッグ |中断](debug---break.md)または ctrl キーを押しながら BREAK キーを押します。

カーネル モードのデバッグでは、キーを押して、ターゲット コンピューターのキーボードからコマンドをキャンセルできます[ **CTRL + C**](ctrl-c--break-.md)します。

使用することができます、 [ **.cls (画面のクリア)** ](-cls--clear-screen-.md)コマンドからテキストをすべてオフに、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 このコマンドは、コマンド全体の履歴を消去します。 使用してコマンドの履歴を消去する、WinDbg で、[編集 |コマンドの出力をクリア](edit---clear-command-output.md)コマンドをクリックしてまたは**コマンドの出力をクリア**デバッガー コマンド] ウィンドウのショートカット メニューの [します。

### <a name="span-idexpressionsyntaxspanspan-idexpressionsyntaxspanexpression-syntax"></a><span id="expression_syntax"></span><span id="EXPRESSION_SYNTAX"></span>式の構文

多くのコマンドおよび拡張機能のコマンドを受け入れる*式*が引数として。 デバッガーは、コマンドを実行する前に、これらの式を評価します。 式の詳細については、[を評価する式](evaluating-expressions.md)を参照してください。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>エイリアス

*エイリアス*は複雑なフレーズを再入力しなくてもすむようにするために使用できるテキスト マクロです。 エイリアスの 2 種類があります。 エイリアスの詳細については、[Using エイリアス](using-aliases.md)を参照してください。

### <a name="span-idselfrepeatingcommandsspanspan-idselfrepeatingcommandsspanself-repeating-commands"></a><span id="self_repeating_commands"></span><span id="SELF_REPEATING_COMMANDS"></span>自己繰り返しコマンド

次のコマンドを使用して、アクションを繰り返したり、条件付きで他のコマンドを実行することができます。

-   [ **J (実行 If-else)** ](j--execute-if---else-.md)条件付きのコマンド

-   [ **Z (実行中に)** ](z--execute-while-.md)条件付きのコマンド

-   [ **~ E (スレッド固有のコマンド)** ](-e--thread-specific-command-.md)コマンド修飾子

-   [ **! 一覧**](-list.md)拡張コマンド

各コマンドの詳細については、個々 のコマンドのトピックを参照してください。

### <a name="span-idcontrollingscrollingspanspan-idcontrollingscrollingspancontrolling-scrolling"></a><span id="controlling_scrolling"></span><span id="CONTROLLING_SCROLLING"></span>スクロールを制御します。

スクロール バーを使用するには、前のコマンドとその出力を表示します。

KD、CDB、またはを使用しているときに任意のキー入力は、下部にある戻るデバッガー コマンド ウィンドウを下に自動的にスクロールします。

、WinDbg で、表示が自動的にスクロール、一番下までコマンドには、出力が生成されます。 または、ENTER キーを押すたびにします。 この自動スクロールを無効にする場合は、クリックして、[オプション](view---options.md)で、**ビュー**メニューと、クリア、**自動スクロール**チェック ボックスをオンします。

### <a name="span-idwindbgtextfeaturesspanspan-idwindbgtextfeaturesspanwindbg-text-features"></a><span id="windbg_text_features"></span><span id="WINDBG_TEXT_FEATURES"></span>WinDbg のテキストの特徴

テキストを表示する方法を変更するいくつかの追加機能を使用する、WinDbg で、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 WinDbg ウィンドウでこれらの機能の一部、デバッガー コマンド ウィンドウでショートカット メニューの一部と適切なメニュー アイコンをクリックしていくつかでアクセスできます。

-   **ワード ラップ**ショートカット メニューのコマンドには、オンとオフは、ワード ラップの状態がオンにします。 このコマンドは、ウィンドウ全体に影響を与える、この状態が変更された後に使用するだけでなくコマンドします。 多くのコマンドと拡張機能は、書式設定された表示を生成するため、通常しないでワード ラップします。

-   [編集 |コマンドの出力に追加](edit---add-to-command-output.md)メニュー コマンドは、デバッガー コマンド ウィンドウでコメントを追加します。 **コマンドの出力に追加**ショートカット メニューのコマンドを同じ効果があります。

-   テキストと、デバッガー コマンド ウィンドウの背景に使用される色をカスタマイズすることができます。 さまざまな種類のテキストを別の色を指定することができます。 別の色でな 1 つの色で出力の自動登録、エラー メッセージを表示するなど、**による DbgPrint**内のメッセージの 3 つ目の色します。 このカスタマイズの詳細については、次を参照してください[ビュー |。オプション](view---options.md)します。

-   フォントのカスタマイズや、特別な編集コマンドを使用してなどの WinDbg のデバッグ情報ウィンドウには、すべての一般的な機能を使用できます。 これらの機能に関する詳細については、[デバッグ情報の Windows を使用して](using-debugging-information-windows.md)を参照してください。

### <a name="span-idremotedebuggingspanspan-idremotedebuggingspanremote-debugging"></a><span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>リモート デバッグ

デバッガーからのリモート デバッグを実行している場合は、コマンドの数に制限がデバッグのクライアントにアクセスできます。 クライアントがアクセスできるコマンドの数を変更するには、使用、 **-clines** [コマンド ライン オプション](command-line-options.md)または\_NT\_デバッグ\_履歴\_サイズ[環境変数](environment-variables.md)します。

 

 





