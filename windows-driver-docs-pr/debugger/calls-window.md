---
title: WinDbg でのコール スタックの表示
description: コマンドを入力するか、または呼び出しのウィンドウを使用して、WinDbg で呼び出し履歴を表示できます。
ms.assetid: 0e5b5611-d43c-40ba-8340-ea49fe18cc3f
keywords:
- デバッグ情報のウィンドウに、ウィンドウを呼び出す
- コール スタック ウィンドウ
- 呼び出し履歴、コール スタック ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09d3d4a6db2f0103c909bd4c61619cf6e4bb069
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374487"
---
# <a name="viewing-the-call-stack-in-windbg"></a>WinDbg でのコール スタックの表示


呼び出し履歴は、プログラム カウンターの現在の場所が原因となった関数呼び出しのチェーンです。 呼び出し履歴の最上位の関数は、現在の関数で、次の関数は、現在の関数を呼び出した関数、という具合です。 表示される呼び出し履歴は、レジスタのコンテキストを変更しない限り、現在のプログラム カウンターに基づいています。 レジスタのコンテキストを変更する方法の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

コマンドを入力するか、または呼び出しのウィンドウを使用して、WinDbg で呼び出し履歴を表示できます。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ


いずれかを入力して、呼び出し履歴を表示することができます、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)デバッガー コマンド ウィンドウでコマンド。

## <a name="span-idcallswindowspanspan-idcallswindowspanspan-idcallswindowspancalls-window"></a><span id="Calls_Window"></span><span id="calls_window"></span><span id="CALLS_WINDOW"></span>コール スタック ウィンドウ


代替方法として、 [ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド、コール スタック ウィンドウで、呼び出し履歴を表示できます。 コール スタック ウィンドウを開くには、次のように選択します。**呼び出し履歴**から、**ビュー**メニュー。

次のスクリーン ショットでは、コール スタック ウィンドウの例を示します。

![コール スタック ウィンドウのスクリーン ショット](images/window-calls.png)

## <span id="ddk_calls_window_dbg"></span><span id="DDK_CALLS_WINDOW_DBG"></span>


コール スタック ウィンドウのボタンを使用すると、呼び出し履歴の表示をカスタマイズできます。 対応する呼び出しの場所に移動する、[ソース ウィンドウ](source-window.md)または[逆アセンブル ウィンドウ](disassembly-window.md)呼び出し履歴の行をダブルクリック、または行を選択し、ENTER キーを押します。 この操作によっても、変更、[ローカル コンテキスト](changing-contexts.md#local-context)選択したスタック フレームにします。 実行中に、またはこのポイントからの詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

ユーザー モードでは、スタック トレースを現在のスレッドのスタックに基づきます。 現在のスレッドのスタックの詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

カーネル モードでは、スタック トレースは、現在の登録コンテキストに基づきます。 特定のスレッド、コンテキストのレコードを一致するように登録するコンテキストを設定したり、フレームをトラップします。 レジスタのコンテキストを設定する方法についての詳細については、次を参照してください。[登録コンテキスト](changing-contexts.md#register-context)します。

コール スタック ウィンドウは、いくつかのボタンを含み、その他のコマンドのショートカット メニューを持つツールバーがあります。 このメニューにアクセスするには、タイトル バーを右クリックしてまたはウィンドウ (右上隅のアイコンをクリックします。![呼び出し ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/tbcall.png)). ツールバーとメニューは、次のボタンおよびコマンドが含まれます。

-   **生の args**関数に渡される最初の 3 つのパラメーターが表示されます。 X86 ベースのプロセッサでは、この表示には、関数 ("Args の子に") に渡される最初の 3 つのパラメーターが含まれます。

-   **Func 情報**フレーム ポインターの省略 (FPO) のデータと関数に関するその他の内部情報が表示されます。 このコマンドは、x86 ベースのプロセッサでのみ使用できます。

-   **ソース**ソース モジュール名と関数名の後に数字を行 (デバッガーにこの情報がある場合) が表示されます。

-   **･ アドレス**フレーム関連のさまざまなアドレスが表示されます。 X86 ベースのプロセッサでは、この表示には、スタック フレーム ("ChildEBP") と戻り値のアドレス ("RetAddr") の基本ポインターが含まれます。

-   **不揮発性 regs**不揮発性レジスタのコンテキストの一部が表示されます。 このコマンドは、Itanium ベースのプロセッサでのみ使用できます。

-   **フレームの nums**フレーム番号が表示されます。 フレームは常に連続した番号、0 から始まります。

-   **引数の型**想定され、スタック内の関数によって受信される引数に関する詳細な情報が表示されます。

-   **常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   **フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジスタのコンテキストとローカル コンテキストの詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 





