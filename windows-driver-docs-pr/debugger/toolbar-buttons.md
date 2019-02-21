---
title: ツール バー ボタン
description: ツール バー ボタン
ms.assetid: a32702fe-28c5-4b41-b4da-9a750946e5dd
keywords:
- ツールバー (WinDbg) ボタンの説明
- ボタン (WinDbg ツールバー) の説明
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedb2317b96cce548b21a95744cf50fed1f5dbc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561008"
---
# <a name="toolbar-buttons"></a>ツール バー ボタン


## <span id="ddk_toolbar_buttons_dbg"></span><span id="DDK_TOOLBAR_BUTTONS_DBG"></span>


を除き、[ブレークポイント] ボタン、ツールバーの各ボタンは、メニュー コマンドと同じです。 各ボタンの影響の詳細については、対応するメニュー コマンドのページを参照してください。

ツールバーのボタンには、次の影響があります。

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
<td align="left"><p>読み取り専用のファイルとソース ファイルを開きます。 等価<a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">ファイル |ソース ファイルを開く</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcut.png" alt="Screen shot of the Cut button" /></td>
<td align="left"><p>アクティブなウィンドウから、選択したテキストを削除し、し、クリップボードに格納します。 等価<a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">編集 |切り取り</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcopy.png" alt="Screen shot of the Copy button" /></td>
<td align="left"><p>アクティブなウィンドウから、選択したテキストをクリップボードにコピーします。 等価<a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">編集 |コピー</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbpaste.png" alt="Screen shot of the Paste button" /></td>
<td align="left"><p>カーソルがある場所をクリップボードにテキストを貼り付けます。 等価<a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">編集 |貼り付け</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p>開始または実行を再開します。 実行は、ブレークポイントに到達する、例外またはイベントの発生、プロセスが終了またはターゲットにデバッガーを中断するまで続行されます。 等価<a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">デバッグ |移動</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p>プロセスの開始時の実行を再開します。 等価<a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">デバッグ |再起動</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p>実行を停止し、ターゲット プロセスを完全に終了します。 等価<a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">デバッグ |デバッグを停止</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p>ユーザー モードでは、このボタンは、プロセスとそのスレッドを停止します。 カーネル モードでは、このボタンは、ターゲット コンピューターに分割します。 デバッガーに制御が返されます。 このボタンは切断すると時間の長い場合に便利です、また<a href="the-debugger-command-window.md" data-raw-source="[Debugger Command window](the-debugger-command-window.md)">デバッガー コマンド ウィンドウ</a>が表示されます。 等価<a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">デバッグ |中断</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p>1 つの命令を実行します。 命令が関数呼び出しの場合は、デバッガーは関数にステップします。 等価<a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">デバッグ |ステップ イン</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p>1 つの命令を実行します。 命令が関数呼び出しの場合は、デバッガーは、1 つの手順で全体の関数を実行します。 等価<a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">デバッグ |ステップ オーバー</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p>現在の関数の残りの部分を実行し、関数の戻り値が完了したときに中断します。 等価<a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">デバッグ |ステップ アウト</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p>アクティブな逆アセンブル ウィンドウまたはソース ウィンドウでマークされている命令までの現在の命令からすべての手順を実行します。 等価<a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">デバッグ |カーソルまで実行</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbbp.png" alt="Screen shot of the Breakpoints button" /></td>
<td align="left"><p><strong>アクティブなウィンドウが、ソースまたは [逆アセンブル] ウィンドウの場合。</strong>現在の行にブレークポイントを挿入します。 (既にある場合、現在の行にブレークポイントを設定、このボタン ブレークポイントを削除します。)</p>
<p><strong>それ以外の場合。</strong>開く、<strong>ブレークポイント</strong>ようなダイアログ ボックス<a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">編集 |ブレークポイント</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Command button" /></td>
<td align="left"><p>アクティブ化を開いたり、<a href="the-debugger-command-window.md" data-raw-source="[Debugger Command](the-debugger-command-window.md)">デバッガー コマンド</a>ウィンドウ。 等価<a href="view---command.md" data-raw-source="[View | Command](view---command.md)">ビュー |コマンド</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>開くか、[ウォッチ] ウィンドウをアクティブにします。 等価<a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">ビュー |ウォッチ</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>開くか、[ローカル] ウィンドウをアクティブにします。 等価<a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">ビュー |[ローカル]</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>開くか、[レジスタ] ウィンドウをアクティブにします。 等価<a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">ビュー |登録</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>新しい [メモリ] ウィンドウを開きます。 等価<a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">ビュー |メモリ</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>開く、または呼び出しのウィンドウを表示します。 等価<a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">ビュー |呼び出し履歴</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>開く、または [逆アセンブル] ウィンドウを表示します。 等価<a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">ビュー |[逆アセンブル]</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>開くか、スクラッチ パッドをアクティブにします。 等価<a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">ビュー |スクラッチ パッド</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbsrcasm.png" alt="Screen shot of the Source Mode button" /></td>
<td align="left"><p>ソース モードおよびモードのアセンブリのデバッグを切り替えます。 オンまたはオフに相当<a href="debug---source-mode.md" data-raw-source="[Debug | Source Mode](debug---source-mode.md)">デバッグ |ソース モード</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbfont.png" alt="Screen shot of the Font button" /></td>
<td align="left"><p>デバッグ情報の windows で使用されるフォントを変更できます。 等価<a href="view---font.md" data-raw-source="[View | Font](view---font.md)">ビュー |フォント</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbopt.png" alt="Screen shot of the Options button" /></td>
<td align="left"><p>表示、<strong>オプション</strong> ダイアログ ボックス。 等価<a href="view---options.md" data-raw-source="[View | Options](view---options.md)">ビュー |オプション</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





