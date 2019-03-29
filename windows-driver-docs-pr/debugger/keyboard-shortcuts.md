---
title: キーボード ショートカット
description: キーボード ショートカット
ms.assetid: 57c16d54-5b7a-4de8-9798-790aac7ec30d
keywords:
- コントロール キー、WinDbg ショートカット キー
- WinDbg、ショートカット キー
- ショートカット キー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: efbdfc75906ef4ecb0f054cd53f071eb0981c5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580061"
---
# <a name="keyboard-shortcuts"></a>キーボード ショートカット


## <span id="ddk_shortcut_keys_dbg"></span><span id="DDK_SHORTCUT_KEYS_DBG"></span>


次のキーボード ショートカットを使用して、ウィンドウを切り替えることができます。 ウィンドウ間を移動する方法の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">キー</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CTRL + TAB</p></td>
<td align="left"><p>デバッグ情報の windows 間で切り替えます。 このキーを繰り返しを使用しているかどうかは、フローティング、ドッキング自体、またはドッキング ウィンドウのタブ付きのコレクションの一部でに関係なく、windows のすべてをスキャンできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt + Tab キー</p></td>
<td align="left"><p>現在、デスクトップ上にある windows の間で切り替えます。 WinDbg のフレームと作成した追加のドッキングの切り替えがこのキーボード ショートカットを使用することもできます。</p></td>
</tr>
</tbody>
</table>

 

マウスの代わりに次のキーボード ショートカットを使用すると、メニュー コマンドを選択します。 各コマンドの詳細については、個々 のコマンドのトピックを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">キー</th>
<th align="left">メニューと同じです。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>F1</p></td>
<td align="left"><p><a href="help---contents.md" data-raw-source="[Help | Contents](help---contents.md)">ヘルプ |内容</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F3</p></td>
<td align="left"><p><a href="edit---find-next.md" data-raw-source="[Edit | Find Next](edit---find-next.md)">編集 |次を検索します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT + F3</p></td>
<td align="left"><p>同じ<a href="edit---find-next.md" data-raw-source="[Edit | Find Next](edit---find-next.md)">編集 |次を検索</a>を除き、逆方向に検索が実行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt + F4</p></td>
<td align="left"><p><a href="file---exit.md" data-raw-source="[File | Exit](file---exit.md)">ファイル |終了</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + F4</p></td>
<td align="left"><p><a href="file---close-current-window.md" data-raw-source="[File | Close Current Window](file---close-current-window.md)">ファイル |現在のウィンドウを閉じる</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F5</p></td>
<td align="left"><p><a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">デバッグ |移動</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT + F5</p></td>
<td align="left"><p><a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">デバッグ |デバッグを停止します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + SHIFT + F5</p></td>
<td align="left"><p><a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">デバッグ |再起動</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>F6</p></td>
<td align="left"><p><a href="file---attach-to-a-process.md" data-raw-source="[File | Attach to a Process](file---attach-to-a-process.md)">ファイル |プロセスにアタッチします。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F7</p></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">デバッグ |カーソルまでを実行します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>F8</p></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">デバッグ |ステップ イン</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F9</p></td>
<td align="left"><p>アクティブなウィンドウが、ソースまたは [逆アセンブル] ウィンドウの場合。現在の行にブレークポイントを挿入します。 (既にある場合、現在の行にブレークポイントを設定、このボタン ブレークポイントを削除します。)</p>
<p>または次の手順を実行してください。開く、<strong>ブレークポイント</strong>ようなダイアログ ボックス<a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">編集 |ブレークポイント</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + F9</p></td>
<td align="left"><p><a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">編集 |ブレークポイント</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F10</p></td>
<td align="left"><p><a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">デバッグ |ステップ オーバー</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl + F10</p></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">デバッグ |カーソルまでを実行します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F11</p></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">デバッグ |ステップ イン</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT + F11</p></td>
<td align="left"><p><a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">デバッグ |ステップ アウト</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 1</p></td>
<td align="left"><p>開く、<a href="debugger-command-window.md" data-raw-source="[Debugger Command window](debugger-command-window.md)">デバッガー コマンド ウィンドウ</a>(と同じ<a href="view---command.md" data-raw-source="[View | Command](view---command.md)">ビュー |コマンド</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 1</p></td>
<td align="left"><p>コマンド ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 2</p></td>
<td align="left"><p>[ウォッチ] ウィンドウを開きます (同じ<a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">ビュー |ウォッチ</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 2</p></td>
<td align="left"><p>[ウォッチ] ウィンドウを閉じます</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 3</p></td>
<td align="left"><p>開く、 <a href="locals-window.md" data-raw-source="[Locals window](locals-window.md)">[ローカル] ウィンドウ</a>(同じ<a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">ビュー |[ローカル]</a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 3</p></td>
<td align="left"><p>[ローカル] ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 4</p></td>
<td align="left"><p>開く、<a href="registers-window.md" data-raw-source="[Registers window](registers-window.md)">レジスタ ウィンドウ</a>(と同じ<a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">ビュー |登録</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 4</p></td>
<td align="left"><p>[レジスタ] ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 5</p></td>
<td align="left"><p>新しい開きます<a href="memory-window.md" data-raw-source="[Memory window](memory-window.md)">メモリ ウィンドウ</a>(と同じ<a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">ビュー |メモリ</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 5</p></td>
<td align="left"><p>[メモリ] ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 6</p></td>
<td align="left"><p>開く、<a href="calls-window.md" data-raw-source="[Calls window](calls-window.md)">コール スタック ウィンドウ</a>(同じ<a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">ビュー |呼び出し履歴</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 6</p></td>
<td align="left"><p>呼び出しのウィンドウを閉じる</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 7</p></td>
<td align="left"><p>開く、<a href="disassembly-window.md" data-raw-source="[Disassembly window](disassembly-window.md)">逆アセンブル ウィンドウ</a>(同じ<a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">ビュー |[逆アセンブル]</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 7</p></td>
<td align="left"><p>[逆アセンブル] ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 8</p></td>
<td align="left"><p>スクラッチ パッドが表示されます (同じ<a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">ビュー |Scratch Pad</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 8</p></td>
<td align="left"><p>スクラッチ パッドを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 9</p></td>
<td align="left"><p>開く、<a href="processes-and-threads-window.md" data-raw-source="[Processes and Threads window](processes-and-threads-window.md)">プロセスとスレッド ウィンドウ</a>(と同じ<a href="view---processes-and-threads.md" data-raw-source="[View | Processes and Threads](view---processes-and-threads.md)">ビュー |プロセスとスレッド</a>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 9</p></td>
<td align="left"><p>プロセスとスレッド ウィンドウを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl + A</p></td>
<td align="left"><p><a href="edit---select-all.md" data-raw-source="[Edit | Select All](edit---select-all.md)">編集 |[すべて選択] します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL キーを押しながら C</p></td>
<td align="left"><p><a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">編集 |コピー</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + D</p></td>
<td align="left"><p><a href="file---open-crash-dump.md" data-raw-source="[File | Open Crash Dump](file---open-crash-dump.md)">ファイル |開いているクラッシュ ダンプ</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL キーを押しながら E キー</p></td>
<td align="left"><p><a href="file---open-executable.md" data-raw-source="[File | Open Executable](file---open-executable.md)">ファイル |開いている実行可能ファイル</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + F</p></td>
<td align="left"><p><a href="edit---find.md" data-raw-source="[Edit | Find](edit---find.md)">編集 |検索</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + G</p></td>
<td align="left"><p><a href="edit---go-to-address.md" data-raw-source="[Edit | Go to Address](edit---go-to-address.md)">編集 |アドレスに移動します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + I</p></td>
<td align="left"><p><a href="file---image-file-path.md" data-raw-source="[File | Image File Path](file---image-file-path.md)">ファイル |イメージ ファイルのパス</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + SHIFT + I</p></td>
<td align="left"><p><a href="edit---set-current-instruction.md" data-raw-source="[Edit | Set Current Instruction](edit---set-current-instruction.md)">編集 |現在の命令を設定します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + K</p></td>
<td align="left"><p><a href="file---kernel-debug.md" data-raw-source="[File | Kernel Debug](file---kernel-debug.md)">ファイル |カーネル デバッグ</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + L</p></td>
<td align="left"><p><a href="edit---go-to-line.md" data-raw-source="[Edit | Go to Line](edit---go-to-line.md)">編集 |行に移動します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl + O</p></td>
<td align="left"><p><a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">ファイル |ソース ファイルを開く</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl + P</p></td>
<td align="left"><p><a href="file---source-file-path.md" data-raw-source="[File | Source File Path](file---source-file-path.md)">ファイル |ソース ファイルのパス</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + R</p></td>
<td align="left"><p><a href="file---connect-to-remote-session.md" data-raw-source="[File | Connect to Remote Session](file---connect-to-remote-session.md)">ファイル |リモート セッションに接続します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl + S</p></td>
<td align="left"><p><a href="file---symbol-file-path.md" data-raw-source="[File | Symbol File Path](file---symbol-file-path.md)">ファイル |シンボル ファイルのパス</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl + V</p></td>
<td align="left"><p><a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">編集 |貼り付け</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + SHIFT + V</p></td>
<td align="left"><p><a href="edit---evaluate-selection.md" data-raw-source="[Edit | Evaluate Selection](edit---evaluate-selection.md)">編集 |選択範囲を評価します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl + W</p></td>
<td align="left"><p><a href="file---open-workspace.md" data-raw-source="[File | Open Workspace](file---open-workspace.md)">ファイル |ワークスペースを開く</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + X</p></td>
<td align="left"><p><a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">編集 |切り取り</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + SHIFT + Y</p></td>
<td align="left"><p><a href="edit---display-selected-type.md" data-raw-source="[Edit | Display Selected Type](edit---display-selected-type.md)">編集 |選択した型の表示</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
ALT +<strong> *</strong> (テンキー)</td>
<td align="left"><p><a href="edit---go-to-current-instruction.md" data-raw-source="[Edit | Go to Current Instruction](edit---go-to-current-instruction.md)">編集 |現在の命令に移動します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>SHIFT + DELETE</p></td>
<td align="left"><p><a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">編集 |切り取り</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT キーを押しながら INSERT</p></td>
<td align="left"><p><a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">編集 |貼り付け</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL キーを押しながら INSERT</p></td>
<td align="left"><p><a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">編集 |コピー</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + BREAK</p></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">デバッグ |Break</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + DEL</p></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">デバッグ |Break</a></p></td>
</tr>
</tbody>
</table>

 

次のショートカット キーは KD に相当/CDB コントロール キー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">キー</th>
<th align="left">メニューと同じです。</th>
<th align="left">KD/CDB キーの制御</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CTRL + ALT + A</p></td>
<td align="left"><p><a href="debug---kernel-connection---cycle-baud-rate.md" data-raw-source="[Debug | Kernel Connection | Cycle Baud Rate](debug---kernel-connection---cycle-baud-rate.md)">デバッグ |カーネルの接続 |ボー レートを切り替える</a></p></td>
<td align="left"><p>Ctrl + A</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + ALT + D</p></td>
<td align="left"></td>
<td align="left"><p><strong><a href="ctrl-d--toggle-debug-info-.md" data-raw-source="[CTRL+D (Toggle Debug Info)](ctrl-d--toggle-debug-info-.md)">CTRL + D (デバッグ情報の表示/非表示)</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + ALT + K</p></td>
<td align="left"><p><a href="debug---kernel-connection---cycle-initial-break.md" data-raw-source="[Debug | Kernel Connection | Cycle Initial Break](debug---kernel-connection---cycle-initial-break.md)">デバッグ |カーネルの接続 |サイクルの初期の中断</a></p></td>
<td align="left"><p>CTRL + K</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + ALT + R</p></td>
<td align="left"><p><a href="debug---kernel-connection---resynchronize.md" data-raw-source="[Debug | Kernel Connection | Resynchronize](debug---kernel-connection---resynchronize.md)">デバッグ |カーネルの接続 |再同期します。</a></p></td>
<td align="left"><p>CTRL + R</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + ALT + V</p></td>
<td align="left"><p><a href="view---verbose-output.md" data-raw-source="[View | Verbose Output](view---verbose-output.md)">ビュー |詳細出力</a></p></td>
<td align="left"><p>Ctrl + V</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + ALT + W</p></td>
<td align="left"><p><a href="view---show-version.md" data-raw-source="[View | Show Version](view---show-version.md)">ビュー |バージョンを表示します。</a></p></td>
<td align="left"><p>Ctrl + W</p></td>
</tr>
</tbody>
</table>

 

ほとんどのデバッグ情報のウィンドウで、キャレット (^) を移動するのに次のキーボード ショートカットを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">カレットの移動</th>
<th align="left">キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 文字左</p></td>
<td align="left"><p>左</p></td>
</tr>
<tr class="even">
<td align="left"><p>右側の 1 つの文字</p></td>
<td align="left"><p>そうです</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1 単語左</p></td>
<td align="left"><p>CTRL + 左</p></td>
</tr>
<tr class="even">
<td align="left"><p>右の単語</p></td>
<td align="left"><p>CTRL + RIGHT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>を整列します。</p></td>
<td align="left"><p>アップ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1 行下へ</p></td>
<td align="left"><p>ダウン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pageup</p></td>
<td align="left"><p>PageUp</p></td>
</tr>
<tr class="even">
<td align="left"><p>Pagedown</p></td>
<td align="left"><p>PageDown</p></td>
</tr>
<tr class="odd">
<td align="left"><p>現在の行の先頭</p></td>
<td align="left"><p>Home</p></td>
</tr>
<tr class="even">
<td align="left"><p>行の末尾</p></td>
<td align="left"><p>END</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイルの先頭</p></td>
<td align="left"><p>Ctrl + Home</p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルの末尾</p></td>
<td align="left"><p>Ctrl + End</p></td>
</tr>
</tbody>
</table>

 

**注**  で、[デバッガー コマンド ウィンドウ](debugger-command-window.md)、上下の方向キーは、コマンド履歴を参照します。 INS キーを使用すると、挿入モードを有効または無効にします。

 

次のキーボード ショートカットを使用して、テキストを選択します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Select</th>
<th align="left">キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左の文字</p></td>
<td align="left"><p>SHIFT + ←</p></td>
</tr>
<tr class="even">
<td align="left"><p>右の文字</p></td>
<td align="left"><p>SHIFT キーを押しながら右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>左の単語</p></td>
<td align="left"><p>SHIFT + CTRL + ←</p></td>
</tr>
<tr class="even">
<td align="left"><p>右の単語</p></td>
<td align="left"><p>SHIFT キー + CTRL + RIGHT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>現在の行</p></td>
<td align="left"><p>Shift キーを押しながら下キャレットが列 1 の場合</p></td>
</tr>
<tr class="even">
<td align="left"><p>上記の行</p></td>
<td align="left"><p>SHIFT + ↑ キャレットが列 1 の場合</p></td>
</tr>
<tr class="odd">
<td align="left"><p>行の末尾に</p></td>
<td align="left"><p>Shift + End</p></td>
</tr>
<tr class="even">
<td align="left"><p>行の先頭に</p></td>
<td align="left"><p>Shift + Home</p></td>
</tr>
<tr class="odd">
<td align="left"><p>を画面します。</p></td>
<td align="left"><p>Shift + PageUp</p></td>
</tr>
<tr class="even">
<td align="left"><p>下の画面します。</p></td>
<td align="left"><p>Shift + PageDown</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイルの先頭に</p></td>
<td align="left"><p>ホーム CTRL + SHIFT +</p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルの末尾に</p></td>
<td align="left"><p>SHIFT キー + CTRL + END</p></td>
</tr>
</tbody>
</table>

 

テキストを削除するのにには、次のキーボード ショートカットを使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DELETE</th>
<th align="left">キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>カレットの右の文字</p></td>
<td align="left"><p>Del</p></td>
</tr>
<tr class="even">
<td align="left"><p>カレットの左の文字</p></td>
<td align="left"><p>BACKSPACE キー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>選択したテキスト</p></td>
<td align="left"><p>Del</p></td>
</tr>
</tbody>
</table>

 

 

 





