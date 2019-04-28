---
title: WinDbg でのアセンブリ コードのデバッグ
description: コマンドを入力するか、[逆アセンブル] ウィンドウを使用して、WinDbg でアセンブリ コードを表示できます。
ms.assetid: e00ea29e-4153-4588-8353-de69910bfc65
keywords:
- デバッグ情報のウィンドウで [逆アセンブル] ウィンドウ
- 逆アセンブル ウィンドウ
- アセンブリを逆アセンブル ウィンドウをデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a6a42777178a219cc1b47a85aed07bb520e1a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363984"
---
# <a name="assembly-code-debugging-in-windbg"></a>WinDbg でのアセンブリ コードのデバッグ


コマンドを入力するか、[逆アセンブル] ウィンドウを使用して、WinDbg でアセンブリ コードを表示できます。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ


アセンブリ コードを表示するにはのいずれかを入力して、 [ **u、ub、uu (Unassemble)** ](u--unassemble-.md)デバッガー コマンド ウィンドウでコマンド。

## <a name="span-idddkdisassemblywindowdbgspanspan-idddkdisassemblywindowdbgspandissasembly-window"></a><span id="ddk_disassembly_window_dbg"></span><span id="DDK_DISASSEMBLY_WINDOW_DBG"></span>Dissasembly ウィンドウ


開くか、逆アセンブル ウィンドウに切り替えて、次のように選択します。 **Dissasembly**から、**ビュー**メニュー。 (ALT + 7 キーを押すこともできます をクリックしてまたは、**逆アセンブリ**ボタン (![[逆アセンブル] ボタンのスクリーン ショット](images/tbdisasm2.png)) ツールバー。 ALT + SHIFT + 7 が閉じます逆アセンブル ウィンドウ。)

次のスクリーン ショットでは、逆アセンブル ウィンドウの例を示します。

![逆アセンブル ウィンドウのスクリーン ショット](images/window-disassembly.png)

デバッガーは、メモリのセクションには、バイナリのマシン命令として解釈し、機械語命令のアセンブリ言語バージョンを生成するためにそれを逆アセンブルします。 結果として得られるコードは、逆アセンブル ウィンドウに表示されます。

[逆アセンブル] ウィンドウには、次の操作を行うことができます。

-   メモリの別のセクションを逆アセンブル、**オフセット**ボックスに、逆アセンブルするメモリのアドレスを入力します。 (アドレスを入力した後、ENTER キーを押しますできますが、する必要はありません)。アドレス; を完了する前に、逆アセンブル ウィンドウはコードを表示します。このコードを無視することができます。

-   メモリの他のセクションを表示するには、次のようにクリックします。、**前**または**次**ボタンまたは PAGEUP または PAGEDOWN キーを押します。 これらのコマンドは、メモリの前または次のセクションからの逆アセンブルしたコードをそれぞれ表示されます。 右方向、左方向、上方向および下方向キーを押して、ウィンドウ内を移動できます。 これらのキーを使用して、ページから移動する場合は、新しいページが表示されます。

[逆アセンブル] ウィンドウには、2 つのボタンとその他のコマンドのショートカット メニューを含むツールバーがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅近くに表示されるアイコンをクリックします。![[逆アセンブル] ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/tbdisasm2.png)). 次の一覧では、メニュー コマンドの一部について説明します。

-   **現在のアドレスに移動して**逆アセンブル ウィンドウで、選択した行に対応し、この行を強調表示するソース ファイルを使用して、ソース ウィンドウを開きます。

-   **現在の命令の前に逆アセンブル**により現在の行に逆アセンブル ウィンドウの中央に配置します。 このコマンドは、既定のオプションです。 このコマンドがオフの場合、現在の行は、逆方向の逆アセンブリがかかるために、時間を節約する逆アセンブル ウィンドウの上部に表示されます。

-   **現在のソース行からの指示を強調表示**が強調表示するのには、現在のソース行に対応する手順については、のすべて。 多くの場合、1 つのソース行は複数のアセンブリ命令に対応します。 コードを最適化すると、これらのアセンブリ命令は、連続する可能性がありますできません。 このコマンドでは、すべての手順については、現在のソース行を使用して組み立てが検索することができます。

-   **各命令のソース行を表示する**各アセンブリ命令に対応するソース行番号を表示します。

-   **各命令のソース ファイルを表示する**各アセンブリ命令に対応するソース ファイル名が表示されます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッグと関連するコマンドとアセンブリの表示の詳細についてが参照アセンブリの詳細については[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

 

 





