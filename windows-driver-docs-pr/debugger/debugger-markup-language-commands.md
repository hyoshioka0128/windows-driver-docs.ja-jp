---
title: デバッガーのマークアップ言語を使用してください。
description: デバッガーのコマンドは、プレーン テキストで、またはデバッガーのマークアップ言語 (DML) を使用する拡張の形式で出力を提供できます。 DML で強化は、出力には、リンクが含まれます。
ms.assetid: 70DDC56F-614F-43B7-B325-91984B74AECF
keywords:
- デバッガーのマークアップ言語
- DML
- 強化されたデバッガー コマンド
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a076a9d17b8eb5626096386b8c96e138091f69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538838"
---
# <a name="using-debugger-markup-language"></a>デバッガーのマークアップ言語を使用してください。


デバッガーのコマンドは、プレーン テキストで、またはデバッガーのマークアップ言語 (DML) を使用する拡張の形式で出力を提供できます。 拡張され、DML に出力には、関連するコマンドを実行することができます をクリックしたリンクが含まれます。

DML では、Windows 10 で使用でき、それ以降です。

**DML 対応コマンド**

次のコマンドは、DML の出力を生成できます。

-   [**.dml\_start**](-dml-start.md)
-   [**.dml\_flow**](-dml-flow.md)
-   [**!dml\_proc**](-dml-proc.md)
-   [**lmD**](lm--list-loaded-modules-.md)
-   [**kM**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
-   [**.chain/D**](-chain--list-debugger-extensions-.md)
-   [**.help/D**](-help--meta-command-help-.md)
-   [**.printf/D**](-printf.md)

[ **LmD** ](lm--list-loaded-modules-.md)コマンドは、DML の出力を提供することのできるコマンドの例を示します。 **LmD**コマンドが読み込まれたモジュールの一覧を表示します。 次の図は、各モジュールの名前は、モジュールに関するより詳細な情報を取得するクリックできるリンクです。

![lmd 出力のスクリーン ショット](images/dmlcommands01.png)

次の図は、クリックした結果を**usbuhci**リンク。 出力には、さらに、usbuhci モジュールの詳細を探索するための他のリンクが含まれています。

![モジュールの詳細のスクリーン ショット](images/dmlcommands02.png)

**DML のオン/オフ**

[ **.Prefer\_dml** ](-prefer-dml.md)コマンドは、オンまたはオフに DML をオンにします。 DML を有効にする場合 (.prefer\_dml 1)、DML を生成することができるコマンド出力が既定で DML の出力が生成されます。

### <a name="span-idconsoleenhancementsspanspan-idconsoleenhancementsspanspan-idconsoleenhancementsspanconsole-enhancements"></a><span id="Console_Enhancements"></span><span id="console_enhancements"></span><span id="CONSOLE_ENHANCEMENTS"></span>コンソールの改良点

DML の解析をサポートしているコマンドの出力領域があるすべての Windows デバッガーのようになりました。 Windbg では、コマンド ウィンドウはすべての DML 動作をサポートし、色、フォント スタイル、およびリンクに表示されます。 コンソール デバッガー、ntsd、cdb、kd、色のモードが有効な場合は true。 コンソールで実行する場合のみ DML、および、唯一のカラー属性をサポートします。 リダイレクトされた I/O のデバッガー、ntsd – d または remote.exe セッションでは、色は表示されません。

### <a name="span-idconsoledebuggercolormodespanspan-idconsoledebuggercolormodespanspan-idconsoledebuggercolormodespanconsole-debugger-color-mode"></a><span id="Console_Debugger_Color_Mode"></span><span id="console_debugger_color_mode"></span><span id="CONSOLE_DEBUGGER_COLOR_MODE"></span>コンソール デバッガーのカラー モード

コンソール デバッガー、ntsd、cdb、kd true コンソールで実行する場合は、色付きの出力を表示する機能があるようになりました。 これは、既定ではありません、カラー モード tools.ini を使用して明示的に有効にする必要があります。 新しい col\_モード&lt;true | false&gt; tools.ini 内のトークンは、[カラー] モード設定を制御します。 Tools.ini と操作の詳細については、次を参照してください[tools.ini を構成する。](configuring-tools-ini.md)

色のモードが有効にすると、デバッガーは、色付きの出力を生成できます。 既定では、ほとんど色が設定されていないと、代わりに既定で現在のコンソールの色。

### <a name="span-idwindbgcommandbrowserwindowspanspan-idwindbgcommandbrowserwindowspanspan-idwindbgcommandbrowserwindowspan-windbg-command-browser-window"></a><span id="_Windbg_Command_Browser_Window"></span><span id="_windbg_command_browser_window"></span><span id="_WINDBG_COMMAND_BROWSER_WINDOW"></span> ブラウザー ウィンドウの Windbg コマンド

Windows 10 およびそれ以降の Windbg では、コマンドのブラウザー ウィンドウは、解析し、DML を表示します。 などのすべてのタグ&lt;リンク&gt;、 &lt;exec&gt;外観の変更が完全にサポートされているとします。

WinDbg でメニューを使用してコマンドのブラウザー セッションを開始するには、次のように選択します。**ビュー**、**コマンド ブラウザー**します。 .Browse&lt;コマンド&gt;でコマンド ウィンドウは、新しいコマンドのブラウザー ウィンドウを開きし、特定のコマンドを実行します。 詳細については、[WinDbg でコマンドのブラウザー ウィンドウを使用して](command-browser-window.md)を参照してください。 Ctrl + n コマンドの新しいブラウザー ウィンドウを開くこともできます。

コマンドのブラウザー ウィンドウには、web ブラウザーで、ドロップダウン リストの歴史と前/次のボタンの動作が意図的には模倣します。 履歴ドロップダウンには、最後の 20 のコマンドのみが表示されますが、コマンドに戻って古い履歴を表示するドロップダウン リストを取得できるように、完全な履歴が保持されます。

多くのコマンド ウィンドウを好きなように、一度に開くことができます。 コマンド ウィンドウがワークスペースに保持されますが、現在のコマンドのみを保存履歴は保持されません。

WinDbg**ビュー**メニューがあります、**ブラウザー Start コマンドを設定**.dml など、最初に、新しいブラウザー ウィンドウの推奨されるコマンドを設定するユーザーのオプション\_を開始します。 このコマンドは、ワークスペースに保存されます。

A**最新コマンド**サブ ウィンドウが 利用可能な**ビュー**関心のあるコマンドを保持するためにメニュー。 最新のコマンドを選択すると、特定のコマンドを使用して新しいブラウザー ウィンドウが開きます。 最新のコマンドの一覧に、ウィンドウの現在のコマンドを追加するブラウザー ウィンドウのコンテキスト メニューにメニュー項目があります。 最新のコマンドの一覧は、ワークスペースに保存されます。

コマンドのブラウザー ウィンドウでは、同期的にコマンドを実行し、コマンドが完了するまで出力は表示されずようにします。 完了するまで、実行時間の長いコマンドは何もを表示されませんが。

リンクでは、web ブラウザーで右クリック コンテキスト メニューのような右クリック コンテキスト メニューがあります。 リンクは、新しいブラウザー ウィンドウで開くことができます。 リンクのコマンドを使用するためのクリップボードにコピーできます。

コマンドのブラウザー ウィンドウを自動更新または手動更新のいずれかに設定するタイトル バーの右上隅の近くのアイコンをクリックします。 自動更新のブラウザーが、デバッガーの状態の変更に、コマンドを再実行して自動的にされます。 これにより、すべての変更でコマンドを実行できますが、ライブ、出力が保持されます。 自動更新が既定でオンにします。 ブラウザーがライブにする必要がない場合は、自動更新を無効にするウィンドウのコンテキスト メニューを使用できます。

などのコマンドはユーザー インターフェイス、ユーザー インターフェイスの特定のコマンドではなく、エンジンによって実行されるので[ **.cls (画面のクリア)**](-cls--clear-screen-.md)コマンドのブラウザーで使用する場合にで構文エラーが返されますwindows とします。 またをユーザー インターフェイスがリモート クライアントと、クライアントではなく、サーバーによって実行されるコマンド、コマンドの出力は、サーバーの状態が表示されます。

ブラウザー ウィンドウのコマンドは、すべてのデバッガー コマンドを実行できます、DML を生成するコマンドを使用することはありません。 ブラウザー ウィンドウを使用すると、コマンドの使用に対してアクティブの任意のセットがあります。

## <a name="span-idcustomizingdmlspanspan-idcustomizingdmlspanspan-idcustomizingdmlspancustomizing-dml"></a><span id="Customizing_DML"></span><span id="customizing_dml"></span><span id="CUSTOMIZING_DML"></span>DML のカスタマイズ


DML では、コマンドの出力に含めることができるタグの小さなセットを定義します。 1 つの例は、&lt;リンク&gt;タグ。 試すことができます、&lt;リンク&gt;タグ (およびその他の DML タグ) を使用して、 [ **.dml\_開始**](-dml-start.md)と[ **.browse**](-browse--display-command-in-browser-.md)コマンド。 コマンドは、 **.browse .dml\_開始** *filepath* DML ファイルに格納されているコマンドを実行します。 出力が表示されます、[コマンド ブラウザー ウィンドウ](command-browser-window.md)通常コマンド ウィンドウではなく。

たとえば、ファイル c:\\DmlExperiment.txt には、次の行が含まれています。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

次のコマンドは、コマンドのブラウザーのウィンドウで、テキストとリンクを表示します。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml ファイル出力のスクリーン ショット](images/dmlcommands03.png)

クリックすると、 **usb で始まるモジュールを一覧表示**リンクでは、次の図のような出力を参照してください。

![モジュールの一覧のスクリーン ショット](images/dmlcommands04.png)

DML のカスタマイズの徹底的に検討すると DML タグの完全な一覧は、[DML を使用してデバッガーの出力のカスタマイズ](customizing-debugger-output-using-dml.md)を参照してください。

 

 





