---
title: ターゲットの制御
description: ターゲットの制御
ms.assetid: bc08b925-2a55-4af6-a5e2-949637a4c7ee
keywords:
- ターゲットを制御します。
- ターゲットの制御の概要
- 開始と停止の対象
- ターゲットの実行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2acf1e476f88b61b83056ae1a3340264d78909f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570745"
---
# <a name="controlling-the-target"></a>ターゲットの制御


## <span id="ddk_controlling_the_target_dbg"></span><span id="DDK_CONTROLLING_THE_TARGET_DBG"></span>


ユーザー モードでのターゲット アプリケーションまたはカーネル モードで対象のコンピュータをデバッグする場合は、ターゲットを指定できます*を実行している*または*停止*します。

使用しない限り、デバッガーが実行されている、ターゲットを離れる、デバッガーは、カーネル モードのターゲットに接続するとき、 **-b** [コマンド ライン オプション](command-line-options.md)、ターゲット システムが応答を停止した (つまり、 *クラッシュ*)、または、ターゲット システムは、以前のカーネル デバッグ操作のため停止されます。

使用しない限り、デバッガーがそのターゲットをすぐに停止、デバッガーが起動するか、ユーザー モードのターゲットに接続するときに、 **-g**コマンド ライン オプション。 詳細については、次を参照してください。[最初のブレークポイント](initial-breakpoint.md)します。

### <a name="span-idwhenthetargetisrunningspanspan-idwhenthetargetisrunningspanwhen-the-target-is-running"></a><span id="when_the_target_is_running"></span><span id="WHEN_THE_TARGET_IS_RUNNING"></span>ターゲットが実行されています。

ターゲットが実行中は、ほとんどのデバッガー アクションは使用できません。

実行中のターゲットを停止する場合を実行できる、**中断**コマンド。 このコマンドにより、デバッガーを*ターゲットに割り込む*します。 つまり、デバッガーが停止して、ターゲット、すべてのコントロールは、デバッガーに与えられます。 アプリケーションはすぐに中断しない可能性があります。 たとえば、すべてのスレッドは、システムのコードを現在実行中または待機操作では、アプリケーションにはコントロールが、アプリケーションのコードに返された後にのみが中断されます。

実行中のターゲットで特定する場合、例外が発生した場合[イベント](controlling-exceptions-and-events.md)が発生した場合、[ブレークポイント](using-breakpoints.md)に達すると、アプリケーションは、ターゲットでは正常に閉じる場合または*デバッガーを中断*. このアクションは、ターゲットを停止し、デバッガーへのすべてのコントロールを提供します。 メッセージが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)エラー、イベント、またはブレークポイントについて説明します。

### <a name="span-idwhenthetargetisstoppedspanspan-idwhenthetargetisstoppedspanwhen-the-target-is-stopped"></a><span id="when_the_target_is_stopped"></span><span id="WHEN_THE_TARGET_IS_STOPPED"></span>ターゲットが停止したときに

開始またはターゲットの実行を制御には、次の操作を行うことができます。

-   アプリケーションが開始する発行を実行して、**移動**コマンド。

-   一度に 1 つのアプリケーションの命令を進めるには、使用、**ステップ イン**または**ステップ オーバー**コマンド。 関数呼び出しが発生した場合**ステップ イン**関数を入力し、それぞれの命令をステップ実行が続行されます。 **ステップ オーバー**関数呼び出しを 1 つのステップとして扱います。 ときに、デバッガーが[モードのアセンブリ](debugging-in-assembly-mode.md)、一度に 1 つのマシン命令が発生したステップ実行します。 ときに、デバッガーが[ソース モード](debugging-in-source-mode.md)、一度に 1 つのソース行が発生したステップ実行します。

-   戻り値が発生した場合、現在の関数と停止を完了するには、使用、**ステップ アウト**または**トレースとウォッチ**コマンド。 **ステップ アウト**コマンドは、現在の関数が終了するまで続きます。 **トレースとウォッチ**まで、現在の関数が終了し、また、関数の呼び出しの概要を表示します。 ただし、発行する必要があります、**トレースとウォッチ**コマンドを対象の関数の最初の命令。

-   例外が発生する場合は使用できます、**例外処理で**と**処理されない例外で**実行を再開し、例外の状態を制御するコマンド。 (例外の詳細については、次を参照してください[を制御する例外とイベント](controlling-exceptions-and-events.md)。)。

-   (WinDbg のみ)内の行を選択した場合、[逆アセンブル ウィンドウ](disassembly-window.md)または[ソース ウィンドウ](source-window.md)しを使用して、**カーソルまで実行**コマンドを選択した行を検出するまでプログラムが実行されます。

-   (ユーザー モードのみ)ターゲット アプリケーションを終了して、最初から再起動しを使用して、**再起動**コマンド。 このコマンドは、デバッガーの作成プロセスでのみ使用できます。 プロセスが再起動されると、すぐに、デバッガーを中断します。

-   (WinDbg のみ)対象アプリケーションを終了し、デバッガーをオフに、使用、**デバッグの停止**コマンド。 このコマンドでは、別のターゲットのデバッグを開始することができます。

### <a name="span-idcommandformsspanspan-idcommandformsspancommand-forms"></a><span id="command_forms"></span><span id="COMMAND_FORMS"></span>コマンドのフォーム

開始またはターゲットの実行を制御するためのほとんどのコマンドは、テキスト コマンド、メニュー コマンド、ツール バー ボタン、およびショートカット キーとして存在します。 基本的なテキスト コマンド、CDB、WinDbg、KD、これらのコマンドを使用することができます。 (コマンドのテキスト形式よくサポート プログラム カウンターの場所の変更や命令の固定数の実行など、追加のオプション。)WinDbg でメニュー コマンド、ツール バー ボタン、およびショートカット キーを使用することができます。

次の形式でコマンドを使用できます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">WinDbg ボタン</th>
<th align="left">WinDbg コマンド</th>
<th align="left">WinDbg のショートカット キー</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">デバッグ |カーソルまでを実行します。</a></p></td>
<td align="left"><p>F7</p>
<p>CTRL + F10</p></td>
<td align="left"><p>(WinDbg のみ)カーソルをマークする行に達するまで実行します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p><a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">デバッグ |デバッグを停止します。</a></p></td>
<td align="left"><p>SHIFT キーを押しながら F5 キーを押して</p></td>
<td align="left"><p>すべてのデバッグを停止し、ターゲットを閉じます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>(CDB/KD のみ) <strong><a href="ctrl-c--break-.md" data-raw-source="[CTRL+C](ctrl-c--break-.md)">CTRL + C</a></strong></p></td>
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">デバッグ |Break</a></p></td>
<td align="left"><p>CTRL + BREAK</p></td>
<td align="left"><p>実行が停止し、ターゲットに、デバッガーは中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-restart--restart-target-application-.md" data-raw-source="[.restart (Restart Target Application)](-restart--restart-target-application-.md)">.restart (ターゲット アプリケーションを再起動)</a></strong></p></td>
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p><a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">デバッグ |再起動</a></p></td>
<td align="left"><p>CTRL + SHIFT + F5</p></td>
<td align="left"><p>(ユーザー モードのみ)ターゲット アプリケーションを再起動します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="g--go-.md" data-raw-source="[g (Go)](g--go-.md)">g (移動)</a></strong></p></td>
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p><a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">デバッグ |移動</a></p></td>
<td align="left"><p>F5</p></td>
<td align="left"><p>ターゲットを自由に実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gc--go-from-conditional-breakpoint-.md" data-raw-source="[gc (Go from Conditional Breakpoint)](gc--go-from-conditional-breakpoint-.md)">gc (条件付きブレークポイントから移動)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>後の実行を再開する<a href="setting-a-conditional-breakpoint.md" data-raw-source="[conditional breakpoint](setting-a-conditional-breakpoint.md)">条件付きブレークポイント</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gh--go-with-exception-handled-.md" data-raw-source="[gh (Go with Exception Handled)](gh--go-with-exception-handled-.md)">gh (例外処理での移動)</a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-handled-exception.md" data-raw-source="[Debug | Go Handled Exception](debug---go-handled-exception.md)">デバッグ |Go は、例外を処理</a></p></td>
<td align="left"></td>
<td align="left"><p>同じ<strong>g (移動)</strong>, 現在の例外が処理済みとして扱われる点が異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gn--gn--go-with-exception-not-handled-.md" data-raw-source="[gn (Go with Exception Not Handled)](gn--gn--go-with-exception-not-handled-.md)">gn (Go 処理されない例外を使用)</a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-unhandled-exception.md" data-raw-source="[Debug | Go Unhandled Exception](debug---go-unhandled-exception.md)">デバッグ |ハンドルされない例外の移動</a></p></td>
<td align="left"></td>
<td align="left"><p>同じ<strong>g (移動)</strong>現在の例外が扱われることを除いて、ハンドルされていないとします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">gu (Go を)</a></strong></p></td>
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p><a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">デバッグ |ステップ アウト</a></p></td>
<td align="left"><p>SHIFT + F11</p></td>
<td align="left"><p>ターゲットは、現在の関数が完了するまで実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="p--step-.md" data-raw-source="[p (Step)](p--step-.md)">p (ステップ)</a></strong></p></td>
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p><a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">デバッグ |ステップ オーバー</a></p></td>
<td align="left"><p>F10</p></td>
<td align="left"><p>ターゲットは、1 つの命令を実行します。 この命令が関数呼び出しの場合は、その関数は、1 つのステップとして実行されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pa--step-to-address-.md" data-raw-source="[pa (Step to Address)](pa--step-to-address-.md)">pa (アドレスに手順)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ターゲットは、指定したアドレスに到達するまで実行します。 この関数のすべての手順が表示されます (ただし、呼び出された関数での手順はありません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="pc--step-to-next-call-.md" data-raw-source="[pc (Step to Next Call)](pc--step-to-next-call-.md)">pc (次の呼び出しにステップ)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>次にターゲットが実行され<strong>呼び出す</strong>命令。 現在の命令の場合、<strong>呼び出す</strong>命令では、この呼び出しが完全に実行され、まで実行が続行されます<strong>呼び出す</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pct--step-to-next-call-or-return-.md" data-raw-source="[pct (Step to Next Call or Return)](pct--step-to-next-call-or-return-.md)">pct (手順を次の呼び出しまたは戻り値)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>達するまで、ターゲットが実行され、<strong>呼び出す</strong>命令または<strong>返す</strong>命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="ph--step-to-next-branching-instruction-.md" data-raw-source="[ph (Step to Next Branching Instruction)](ph--step-to-next-branching-instruction-.md)">ph (分岐命令を次に手順)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ターゲットでは、任意の種類の条件付きなどの分岐命令に到達または無条件分岐、呼び出しから制御が戻るし、システムの呼び出しまで実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pt--step-to-next-return-.md" data-raw-source="[pt (Step to Next Return)](pt--step-to-next-return-.md)">pt (戻り値を次に手順)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>達するまで、ターゲットが実行され、<strong>返す</strong>命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="t--trace-.md" data-raw-source="[t (Trace)](t--trace-.md)">t (トレース)</a></strong></p></td>
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">デバッグ |ステップ イン</a></p></td>
<td align="left"><p>F11</p>
<p>F8</p></td>
<td align="left"><p>ターゲットは、1 つの命令を実行します。 この命令が関数呼び出しの場合は、デバッガーはその呼び出しをトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="ta--trace-to-address-.md" data-raw-source="[ta (Trace to Address)](ta--trace-to-address-.md)">ta (アドレスに Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ターゲットは、指定したアドレスに到達するまで実行します。 この関数と呼び出された関数のすべての手順が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tb--trace-to-next-branch-.md" data-raw-source="[tb (Trace to Next Branch)](tb--trace-to-next-branch-.md)">tb (次の分岐に Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(すべてモード、x86 ベースのシステムでのみ、カーネル モードを除く)ターゲットは、次の分岐命令に到達するまで実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="tc--trace-to-next-call-.md" data-raw-source="[tc (Trace to Next Call)](tc--trace-to-next-call-.md)">tc (次の呼び出しをトレース)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>次にターゲットが実行され<strong>呼び出す</strong>命令。 現在の命令の場合、<strong>呼び出し</strong>新しいまで命令、命令がトレースに<strong>呼び出し</strong>に達した。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tct--trace-to-next-call-or-return-.md" data-raw-source="[tct (Trace to Next Call or Return)](tct--trace-to-next-call-or-return-.md)">tct (トレースを次の呼び出しまたは戻り値に)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>達するまで、ターゲットが実行され、<strong>呼び出す</strong>命令または<strong>返す</strong>命令。 現在の命令の場合、<strong>呼び出す</strong>命令または<strong>を返す</strong>新しいまで命令、命令がトレースに<strong>呼び出す</strong>または<strong>を返す</strong>に到達します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="th--trace-to-next-branching-instruction-.md" data-raw-source="[th (Trace to Next Branching Instruction)](th--trace-to-next-branching-instruction-.md)">th (次の分岐命令に Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ターゲットでは、任意の種類の条件付きなどの分岐命令に到達または無条件分岐、呼び出しから制御が戻るし、システムの呼び出しまで実行します。 現在の命令が分岐命令の場合は、新しい分岐命令に到達するまでに、命令がトレースされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tt--trace-to-next-return-.md" data-raw-source="[tt (Trace to Next Return)](tt--trace-to-next-return-.md)">tt ([次へ] を返す Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>達するまで、ターゲットが実行され、<strong>返す</strong>命令。 現在の命令の場合、<strong>返す</strong>新しいまで命令、命令がトレースに<strong>返す</strong>に達する。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="wt--trace-and-watch-data-.md" data-raw-source="[wt (Trace and Watch Data)](wt--trace-and-watch-data-.md)">wt (トレースとデータの監視)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ターゲットをまったく指定された関数が完了するまで実行します。 統計情報が表示されます。</p></td>
</tr>
</tbody>
</table>

 

ターゲット コンピューターを再起動する方法の詳細については、次を参照してください。[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)します。

### <a name="span-idcommandlineoptionsspanspan-idcommandlineoptionsspancommand-line-options"></a><span id="command_line_options"></span><span id="COMMAND_LINE_OPTIONS"></span>コマンド ライン オプション

アプリケーションを開始または読み込むときにすぐに停止したくない場合は、CDB またはと共に WinDbg を使用して、 **-g**コマンド ライン オプション。 このような状況の詳細については、次を参照してください。[最初のブレークポイント](initial-breakpoint.md)します。

CDB および WinDbg もサポートして、 **-g** [コマンド ライン オプション](command-line-options.md)します。 このオプションでは、デバッグ セッションをアプリケーションが正しく完了した場合を終了します。

次のコマンドが最初から最後まで、アプリケーションを実行しようし、エラーが発生した場合にのみ、デバッガーのプロンプトが表示されます。

```console
cdb -g -G ApplicationName 
```

使用することができます、 **-pt** [コマンド ライン オプション](command-line-options.md)区切りのタイムアウトを設定します。デバッガーと通信できません。 ターゲットが可能な特定の問題があります。 Break コマンドが発行され、この時刻より後、ターゲットに、デバッガーが中断できない場合、デバッガーには、「侵入がタイムアウトしました」のメッセージが表示されます。

この時点では、ターゲットに分割しようとしています。 デバッガーが停止します。 代わりに、デバッガーは、ターゲットを一時停止し、対象アプリケーションを調べる (は制御) することができます。

既定のタイムアウトは 30 秒です。

 

 





