---
title: ブレークポイントを制御するメソッド
description: ブレークポイントを制御するメソッド
ms.assetid: 69de05e8-1b41-403a-a628-88da9528e1ab
keywords:
- ブレークポイントを制御します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74e0d81622a613334ca2548b69bbd6b231e4ef8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352445"
---
# <a name="methods-of-controlling-breakpoints"></a>ブレークポイントを制御するメソッド


仮想アドレスやモジュールとルーチンのオフセット (ソース モード) の場合、ソース ファイルと行番号では、ブレークポイントの場所を指定できます。 オフセットなしのルーチンにブレークポイントを配置する場合は、ルーチンが入力されると、ブレークポイントがアクティブになります。

ブレークポイントのいくつか追加の種類があります。

-   ブレークポイントは、特定のスレッドを関連付けることができます。

-   ブレークポイント、トリガーは、前に、固定数のアドレスを通過できるようにします。

-   ブレークポイントがトリガーされると、特定のコマンドを自動的に発行できます。

-   ブレークポイントは、非実行可能ファイルのメモリと読み取りまたは書き込みをするのには、その場所へのウォッチを設定できます。

ユーザー モードでは、複数のプロセスをデバッグする場合、ブレークポイントのコレクションは、現在のプロセスに依存します。 を表示または変更するプロセスのブレークポイントは、現在のプロセスとしてプロセスを選択する必要があります。 現在のプロセスの詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

### <a name="span-idmethodsofcontrollinganddisplayingbreakpointsspanspan-idmethodsofcontrollinganddisplayingbreakpointsspandebugger-commands-for-controlling-and-displaying-breakpoints"></a><span id="methods_of_controlling_and_displaying_breakpoints"></span><span id="METHODS_OF_CONTROLLING_AND_DISPLAYING_BREAKPOINTS"></span>制御して、ブレークポイントを表示するためのデバッガー コマンド

コントロールまたは、ブレークポイントの表示するには、次のメソッドを使用できます。

-   使用して、 [ **bl (ブレークポイントの一覧)** ](bl--breakpoint-list-.md)既存のブレークポイントと現在の状態を一覧表示するコマンド。

-   使用して、 [ **.bpcmds (ブレークポイント コマンドが表示)** ](-bpcmds--display-breakpoint-commands-.md)と共にそれらを作成するために使用されたコマンドのすべてのブレークポイントの一覧を表示するコマンド。

-   使用して、 [ **bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)新しいブレークポイントを設定するコマンド。

-   使用して、 [ **bu (未解決のブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)新しいブレークポイントを設定するコマンド。 設定されているブレークポイント**bu**未解決ブレークポイントが呼び出される異なる特性が設定されているブレークポイントがある**bp**します。 詳細については、次を参照してください。[未解決ブレークポイント (bu ブレークポイント)](unresolved-breakpoints---bu-breakpoints-.md)します。

-   使用して、 [ **bm (シンボルのブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドを指定したパターンに一致するシンボルに新しいブレークポイントを設定します。 ブレークポイントを設定**bm**アドレスに関連付けられます (など、 **bp**ブレークポイント) 場合、 **/d**スイッチが含まれています解決とが (など、 **bu。** ブレークポイント) このスイッチが含まれていない場合。

-   使用して、 [ **ba (アクセスの切断)** ](ba--break-on-access-.md)を設定するコマンド、*プロセッサ ブレークポイント*とも呼ばれます、*データ ブレークポイント*します。 または、コードとして実行されると、読み取り時に、カーネルの I/O が発生した場合、メモリ位置が書き込まれるときに、これらのブレークポイントをトリガーできます。 詳細については、次を参照してください。[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)します。

-   使用して、 [ **bc (ブレークポイント クリア)** ](bc--breakpoint-clear-.md)コマンドを完全に 1 つ以上のブレークポイントを削除します。

-   使用して、 [ **(ブレークポイントを無効にする) bd** ](bd--breakpoint-disable-.md)コマンド 1 つ以上のブレークポイントを一時的に無効にします。

-   使用して、 [ **(ブレークポイントを有効にする) をする**](be--breakpoint-enable-.md)コマンドを 1 つまたは複数の無効なブレークポイントを再度有効にします。

-   使用して、 [ **br (ブレークポイント番号)** ](br--breakpoint-renumber-.md)コマンドを既存のブレークポイントの ID を変更します。

-   使用して、 [ **bs (更新プログラムはブレークポイント コマンド)** ](bs--update-breakpoint-command-.md)を既存のブレークポイントに関連付けられているコマンドを変更するコマンド。

-   使用して、 [ **bsc (更新プログラムの条件付きブレークポイント)** ](bsc--update-conditional-breakpoint-.md)既存の条件付きブレークポイントが発生する条件を変更するコマンド。

Visual Studio および WinDbg では、いくつかのユーザー インターフェイス要素を制御し、ブレークポイントの表示を容易にします。 参照してください[Visual Studio でブレークポイントを設定](setting-breakpoints-in-visual-studio.md)と[WinDbg にブレークポイントを設定](setting-breakpoints-in-windbg.md)します。

各ブレークポイントが関連付けられているブレークポイント ID と呼ばれる 10 進数です。 この番号は、さまざまなコマンドのブレークポイントを識別します。

### <a name="span-idbreakpointcommandsspanspan-idbreakpointcommandsspanbreakpoint-commands"></a><span id="breakpoint_commands"></span><span id="BREAKPOINT_COMMANDS"></span>コマンドのブレークポイント

ブレークポイントがヒットしたときに自動的に実行がブレークポイントでは、コマンドを含めることができます。 たとえば、次のコマンドは MyFunction + 0x47 で中断、ダンプ ファイルを書き込み、し、実行を再開します。

```dbgcmd
0:000> bu MyFunction+0x47 ".dump c:\mydump.dmp; g" 
```

**注**  カーネル デバッガーからユーザー モード デバッガーの制御を行う場合は使用しないで[ **g (移動)** ](g--go-.md)ブレークポイント コマンド文字列にします。 シリアル インターフェイスは、このコマンドでは、対応できない可能性があります、CDB を分割することはできません。 このような状況の詳細については、次を参照してください。[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

 

### <a name="span-idnumberofbreakpointsspanspan-idnumberofbreakpointsspannumber-of-breakpoints"></a><span id="number_of_breakpoints"></span><span id="NUMBER_OF_BREAKPOINTS"></span>ブレークポイントの数

カーネル モードでは、最大 32 のソフトウェアのブレークポイントを使用できます。 ユーザー モードでは、任意の数のソフトウェアのブレークポイントを使用できます。

サポートされているプロセッサのブレークポイントの数は、ターゲット プロセッサ アーキテクチャに依存します。

### <a name="span-idconditionalbreakpointsspanspan-idconditionalbreakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件付きブレークポイント

特定の条件下でのみトリガーされるブレークポイントを設定できます。 これらのブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

 

 





