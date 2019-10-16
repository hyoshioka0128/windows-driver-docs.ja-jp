---
title: ツール バー ボタン
description: ツール バー ボタン
ms.assetid: a32702fe-28c5-4b41-b4da-9a750946e5dd
keywords:
- ツールバー (WinDbg)、ボタンの説明
- ボタン (WinDbg ツールバー)、説明
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedb2317b96cce548b21a95744cf50fed1f5dbc2
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323597"
---
# <a name="toolbar-buttons"></a>ツール バー ボタン


## <span id="ddk_toolbar_buttons_dbg"></span><span id="DDK_TOOLBAR_BUTTONS_DBG"></span>


[ブレークポイント] ボタンを除き、ツールバーの各ボタンはメニューコマンドと同じです。 各ボタンの効果の詳細については、対応するメニューコマンドのページを参照してください。

ツールバーのボタンには、次のような効果があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Button</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>ソースファイルを読み取り専用ファイルとして開きます。 File | と同じです。 <a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">ソースファイルを開き</a>ます。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcut.png" alt="Screen shot of the Cut button" /></td>
<td align="left"><p>選択したテキストをアクティブウィンドウから削除し、クリップボードに配置します。 Edit と同じです<a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">|。切り取り</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcopy.png" alt="Screen shot of the Copy button" /></td>
<td align="left"><p>選択したテキストをアクティブウィンドウからクリップボードにコピーします。 Edit と同じです<a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">|。コピー</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbpaste.png" alt="Screen shot of the Paste button" /></td>
<td align="left"><p>カーソルが置かれている場所にクリップボードのテキストを貼り付けます。 Edit と同じです<a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">|。貼り付け</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p>実行を開始または再開します。 実行は、ブレークポイントに達するか、例外またはイベントが発生するか、プロセスが終了するか、デバッガーがターゲットに中断するまで続行されます。 Debug | と同じです。 <a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">を参照</a>してください。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p>プロセスの開始時に実行を再開します。 Debug | と同じです。 <a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">を再起動</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p>実行を停止し、ターゲットプロセスを完全に終了します。 Debug | と同じです。 <a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">デバッグを停止</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p>ユーザーモードでは、このボタンをクリックすると、プロセスとそのスレッドが停止します。 カーネルモードでは、このボタンは対象のコンピューターに分割されます。 制御がデバッガーに返されます。 このボタンは、長い<a href="the-debugger-command-window.md" data-raw-source="[Debugger Command window](the-debugger-command-window.md)">デバッガーコマンドウィンドウ</a>表示をオフにする場合にも役立ちます。 Debug | と同じです。 <a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">中断</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p>1つの命令を実行します。 命令が関数呼び出しの場合、デバッガーは関数にステップインします。 Debug | と同じです。 <a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">ステップイン</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p>1つの命令を実行します。 命令が関数呼び出しの場合、デバッガーは関数全体を1回の手順で実行します。 Debug | と同じです。 <a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">ステップオーバー</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p>現在の関数の残りの部分を実行し、関数の戻りが完了したときに中断します。 Debug | と同じです。 <a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">ステップアウト</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p>[アクティブな逆アセンブリ] ウィンドウまたはソースウィンドウでマークされている命令まで、現在の命令からすべての命令を実行します。 Debug | と同じです。 <a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">カーソルまで実行</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbbp.png" alt="Screen shot of the Breakpoints button" /></td>
<td align="left"><p><strong>アクティブウィンドウがソースウィンドウまたは逆アセンブルウィンドウである場合は、次のようになります。</strong>現在の行にブレークポイントを挿入します。 (現在の行にブレークポイントが既に設定されている場合、このボタンをクリックするとブレークポイントが削除されます)。</p>
<p><strong>それ以外の場合:</strong>Edit | のような [<strong>ブレークポイント</strong>] ダイアログボックスを開きます。 <a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">ブレークポイント</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Command button" /></td>
<td align="left"><p><a href="the-debugger-command-window.md" data-raw-source="[Debugger Command](the-debugger-command-window.md)">デバッガーのコマンド</a>ウィンドウを開いたり、アクティブにしたりします。 View | と同じです。 <a href="view---command.md" data-raw-source="[View | Command](view---command.md)">コマンド</a>を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>ウォッチウィンドウを開くか、またはアクティブ化します。 View | と同じです。 <a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">Watch</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>[ローカル] ウィンドウを開いたり、アクティブにしたりします。 View | と同じです。 <a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">[ローカル</a>]。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>[レジスタ] ウィンドウを開いたり、アクティブにしたりします。 View | と同じです。 <a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">レジスタ</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>新しいメモリウィンドウを開きます。 View | と同じです。 <a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">メモリ</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>呼び出しウィンドウを開いたり、アクティブにしたりします。 View | と同じです。 <a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">呼び出し履歴</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>[逆アセンブル] ウィンドウを開いたり、アクティブにしたりします。 View | と同じです。 <a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">逆アセンブリ</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>スクラッチパッドを開くか、アクティブにします。 View | と同じです。 <a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">スクラッチパッド</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbsrcasm.png" alt="Screen shot of the Source Mode button" /></td>
<td align="left"><p>ソースモードとアセンブリモードのデバッグを切り替えます。 デバッグ | を選択またはクリアする場合と同じです。 <a href="debug---source-mode.md" data-raw-source="[Debug | Source Mode](debug---source-mode.md)">ソースモード</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbfont.png" alt="Screen shot of the Font button" /></td>
<td align="left"><p>デバッグ情報ウィンドウで使用されるフォントを変更できます。 View | と同じです。 <a href="view---font.md" data-raw-source="[View | Font](view---font.md)">フォント</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbopt.png" alt="Screen shot of the Options button" /></td>
<td align="left"><p>[<strong>オプション</strong>] ダイアログボックスを表示します。 View | と同じです。 <a href="view---options.md" data-raw-source="[View | Options](view---options.md)">オプション</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





