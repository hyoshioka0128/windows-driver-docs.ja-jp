---
title: ソース モードでのデバッグ
description: ソース モードでのデバッグ
ms.assetid: b236f53b-2429-4085-b008-6648d1474ec2
keywords:
- ソースのデバッグ
- ソース モード
- ソースのデバッグの概要
- ビルド ユーティリティ (build.exe) 回避の最適化
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0264517c0956a00dee2d59cff3c17078856963b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581564"
---
# <a name="debugging-in-source-mode"></a>ソース モードでのデバッグ


## <span id="ddk_debugging_in_source_mode_dbg"></span><span id="DDK_DEBUGGING_IN_SOURCE_MODE_DBG"></span>


アプリケーションのデバッグは、逆アセンブルされたバイナリではなく、コードのソースを分析する場合に簡単です。

WinDbg、KD、CDB は、ソース言語が C#、C++、またはアセンブリの場合でデバッグするには、ソース コードを使用することができます。

### <a name="span-idcompilationrequirementsspanspan-idcompilationrequirementsspancompilation-requirements"></a><span id="compilation_requirements"></span><span id="COMPILATION_REQUIREMENTS"></span>コンパイルの要件

使用するソースのデバッグ、する必要がありますが、コンパイラまたはリンカーのシンボル ファイル (.pdb ファイル) を作成、バイナリが構築されます。 これらのシンボル ファイルは、バイナリの命令がソース行に対応させる方法をデバッガーに表示します。

シンボル ファイルに実際のソース テキストが含まれていないために、デバッガーは実際のソース ファイルにアクセスすることがあります。

可能な場合は、コンパイラとリンカーする必要がありますいないにコードを最適化します。 ソースのデバッグとローカル変数へのアクセスより難しくなると、コードが最適化されている場合、場合によってほとんど不可能です。 コンパイラおよびリンカーとしてビルド ユーティリティを使用する場合の設定、MSC\_最適化マクロを **/Od/Oi**最適化を回避するためにします。

### <a name="span-idlocatingthesymbolfilesandsourcefilesspanspan-idlocatingthesymbolfilesandsourcefilesspanlocating-the-symbol-files-and-source-files"></a><span id="locating_the_symbol_files_and_source_files"></span><span id="LOCATING_THE_SYMBOL_FILES_AND_SOURCE_FILES"></span>シンボル ファイルおよびソース ファイルを検索します。

を元のモードでデバッグするには、デバッガーは、ソース ファイルとシンボル ファイルを検索できる必要があります。 詳細については、次を参照してください。[ソース コード](source-code.md)します。

### <a name="span-idbeginningsourcedebuggingspanspan-idbeginningsourcedebuggingspanbeginning-source-debugging"></a><span id="beginning_source_debugging"></span><span id="BEGINNING_SOURCE_DEBUGGING"></span>ソースのデバッグを開始

デバッガーは、適切なシンボル ファイルとは、現在デバッグ中のスレッドのソース ファイルがあるときに、ソース情報を表示できます。

新しいユーザー モード アプリケーションを起動するには、デバッガーを使用して、Ntdll.dll、アプリケーションの読み込み時に、初期の中断が発生します。 デバッガーには、Ntdll.dll のソース ファイルへのアクセスがあるない、ためこの時点で、アプリケーションのソースの情報にアクセスできません。

プログラムをアプリケーションの先頭にカウンターを移動するには、バイナリのエントリ ポイントでブレークポイントを追加します。 [デバッガー コマンド ウィンドウ](debugger-command-window.md)、次のコマンドを入力します。

```dbgcmd
bp main
g
```

アプリケーションが、読み込まれ、停止した、**メイン**関数を入力します。 (もちろん、だけでなく、すべてのエントリ ポイントを使用することができます**メイン**)。

アプリケーションでは、例外をスローする場合は、デバッガーを中断します。 ソースの情報はこの時点で使用できます。 ただし、改行を使用して発行する場合、 [ **CTRL + C**](ctrl-c--break-.md)、 [CTRL + BREAK](debug---break.md)、またはデバッグ |Break コマンド、デバッガーは、ソース コードが表示されないように、新しいスレッドを作成します。

ソース ファイルのあるスレッドに達した後は、ソースのデバッグ コマンドを実行するのにデバッガー コマンド ウィンドウを使用できます。 WinDbg を使用している場合、[ソース ウィンドウ](source-window.md)が表示されます。 クリックして、ソース ウィンドウを既に開いているかどうかは**ソース ファイルを開く**上、**ファイル**メニュー、WinDbg は通常、ソースの新しいウィンドウを作成します。 デバッグ プロセス与えず、前のウィンドウを閉じることができます。

### <a name="span-idsourcedebugginginthewindbgguispanspan-idsourcedebugginginthewindbgguispansource-debugging-in-the-windbg-gui"></a><span id="source_debugging_in_the_windbg_gui"></span><span id="SOURCE_DEBUGGING_IN_THE_WINDBG_GUI"></span>WinDbg の GUI でソースのデバッグ

WinDbg を使用している場合は、プログラム カウンターは、デバッガーからの情報をソース コードがすぐにソース ウィンドウが表示されます。

WinDbg では、開かれた WinDbg またはするソース ファイルごとに 1 つのソース ウィンドウが表示されます。 このウィンドウのテキスト プロパティの詳細については、次を参照してください。[ソース Windows](source-window.md)します。

アプリケーションのステップ、または、ブレークポイントまたはカーソルを実行することができます。 ステップ実行とトレース コマンドの詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

ソース モードでは、アプリケーションをステップ実行するように適切なソース ウィンドウがフォア グラウンドに移動します。 デバッガーを移動する可能性がありますも、アプリケーションの実行中に呼び出されるルーチンを Microsoft Windows はであるため、[逆アセンブル ウィンドウ](disassembly-window.md)フォア グラウンド (デバッガーがあるないために、この種類の呼び出しが発生したときにアクセスをこれらの関数のソースに)。 既知のソース ファイルに戻ると、プログラム カウンターが、適切なソース ウィンドウがアクティブになります。

アプリケーションの間を移動し、WinDbg には、ソース ウィンドウと [逆アセンブル] ウィンドウ内の場所が強調表示されます。 ブレークポイントが設定される行も強調表示されます。 ソース コードは、言語の解析に合わせて色付けされます。 ソース ウィンドウが選択されている場合、シンボルを評価するには、マウスを合わせることができます。 これらの機能とそれらを制御する方法の詳細については、次を参照してください。[ソース Windows](source-window.md)します。

WinDbg でソース モードを有効にするには、使用、 [ **l + t** ](l---l---set-source-options-.md)コマンドで、をクリックして**ソース モード**上、**デバッグ** メニューの [または] をクリックして、 **ソース モード**ボタン (![ボタンをソース モードのスクリーン ショット](images/tbsrc.png)) ツールバー。

ソース モードがアクティブの場合、 **ASM**ステータス バーで使用できなくなったインジケーターが表示されます。

表示したり、元のモードでの関数をステップ実行するように、任意のローカル変数の値を変更することができます。 詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

### <a name="span-idsourcedebugginginthedebuggercommandwindowspanspan-idsourcedebugginginthedebuggercommandwindowspansource-debugging-in-the-debugger-command-window"></a><span id="source_debugging_in_the_debugger_command_window"></span><span id="SOURCE_DEBUGGING_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>ソースのデバッガー コマンド ウィンドウでデバッグ

CDB を使用している場合は、別のソース ウィンドウがありません。 ただし、ソースをステップ実行すると、進行状況を表示もできます。

実行する前にソース CDB でのデバッグ、発行することによってソース行のシンボルを読み込む必要が、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンドまたはでデバッガーを起動して、 [ **-コマンド ライン オプションを行**](cdb-command-line-options.md)します。

実行する場合、 [ **l + t** ](l---l---set-source-options-.md)コマンドをすべてのプログラムのステップ実行は 1 つずつ実行時、ソース行。 使用**l t**一度に 1 つのアセンブリ命令にステップ インします。 このコマンドがオンまたはオフにすると同じ効果を持つ WinDbg を使用している場合**ソース モード**で、**デバッグ**メニューまたはツールバーのボタンを使用します。

[ **L + s** ](l---l---set-source-options-.md)コマンド プロンプトで、現在のソース行と行番号を表示します。 行番号のみを表示する場合を使用して、 **l + l**代わりにします。

使用する場合[ **l o** ](l---l---set-source-options-.md)と**l + s**プログラムをステップ実行するときに、ソース行のみが表示されます。 プログラム カウンター、逆アセンブリ コード、および登録情報は表示されません。 この種の表示を使用すると、すばやくコードをステップ実行し、ソースが何も表示できます。

使用することができます、 [ **lsp (設定数のソース行)** ](lsp--set-number-of-source-lines-.md)またはステップ実行、アプリケーションを実行するときにソース行の数を表示する正確に指定するコマンド。

次のコマンド シーケンスは、ソース ファイルをステップ効果的な方法です。

```text
.lines        enable source line information
bp main       set initial breakpoint
l+t           stepping will be done by source line
l+s           source lines will be displayed at prompt
g             run program until "main" is entered
pr            execute one source line, and toggle register display off
p             execute one source line 
```

[ **」と入力**](enter--repeat-last-command-.md)繰り返します最後のコマンドを今すぐ、ENTER キーを使用してアプリケーションをステップことができます。 各手順では、ソース行、メモリのオフセット、およびアセンブリのコードを表示します。

逆アセンブリの表示を解釈する方法の詳細については、次を参照してください。[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

アセンブリ コードが表示されたら、行の右端にアクセスされているメモリの任意の場所が表示されます。 使用することができます、 [ **d\* (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)と[ **e\* (値を入力してください)** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンドを表示または変更しますこれらの場所の値。

オフセットまたはメモリについては、使用を判断するには、各アセンブリ命令を表示しなければならない場合[ **l t** ](l---l---set-source-options-.md)ソース行ではなくアセンブリ命令ごとにステップ インします。 ソース行の情報を表示もできます。 各ソース行は、1 つまたは複数のアセンブリ命令に対応します。

これらすべてのコマンドは WinDbg および CDB 使用できます。 WinDbg からのソース行情報を表示するコマンドを使用する[デバッガー コマンド ウィンドウ](debugger-command-window.md)の代わりに、ソース ウィンドウから。

### <a name="span-idsourcelinesandoffsetsspanspan-idsourcelinesandoffsetsspansource-lines-and-offsets"></a><span id="source_lines_and_offsets"></span><span id="SOURCE_LINES_AND_OFFSETS"></span>ソース行とオフセット

ソースの特定のソース行に対応するオフセットを決定する、式エバリュエーターを使用してデバッグを実行することもできます。

次のコマンドは、メモリのオフセットを表示します。

```dbgcmd
? `[[module!]filename][:linenumber]` 
```

省略した場合*filename*デバッガーが現在のプログラム カウンターに対応するソース ファイルを検索します。

デバッガーを読み取り*linenumber* 10 進数として番号を追加しない限り**0 x**現在の既定の基数に関係なく、その前にします。 省略した場合*linenumber*、ソース ファイルに対応する実行可能ファイルの初期のアドレスに、式が評価されます。

この構文が場合にのみ、CDB で認識、 **.lines**コマンドまたは **-行**コマンド ライン オプションには、ソース行のシンボルが読み込まれています。

この手法は、プログラム カウンターが指しているに関係なく使用するため、非常に多様です。 たとえば、この手法には、次などのコマンドを使用して、事前にブレークポイントを設定することができます。

```dbgcmd
bp `source.c:31` 
```

詳細については、次を参照してください。[ソース行構文](source-line-syntax.md)と[を使用してブレークポイント](using-breakpoints.md)します。

### <a name="span-idsteppingandtracinginsourcemodespanspan-idsteppingandtracinginsourcemodespanstepping-and-tracing-in-source-mode"></a><span id="stepping_and_tracing_in_source_mode"></span><span id="STEPPING_AND_TRACING_IN_SOURCE_MODE"></span>ステップ実行し、元のモードでのトレース

元のモードでデバッグする場合があります複数の関数呼び出しを 1 つのソース行にします。 使用することはできません、 **p**と**t**これらを分離するためのコマンドは関数呼び出し。

たとえば、次のコマンドで、 **t**コマンドの両方にステップ イン**GetTickCount**と**printf**中、 **p**コマンドをステップ オーバー両方の関数呼び出し。

```cpp
printf( "%x\n", GetTickCount() );
```

トレース中に特定の呼び出し経由でその他の呼び出しにステップ インする場合は、使用[ **.step\_フィルター (ステップ フィルターの設定)** ](-step-filter--set-step-filter-.md)を経由での手順への呼び出しを示します。

使用することができます**\_手順\_フィルター** framework 機能 (Microsoft Foundation Classes (MFC) や Active Template Library (ATL) の呼び出しなど) をフィルター処理します。

 

 





