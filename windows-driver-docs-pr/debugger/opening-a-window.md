---
title: ウィンドウを開く
description: ウィンドウを開く
ms.assetid: e056a556-8201-47e5-9a21-dbd5277c15c2
keywords:
- 情報のデバッグ ウィンドウで開く
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea21ae1b5260054952c351bdb7bfbe60fce2ecfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538344"
---
# <a name="opening-a-window"></a>ウィンドウを開く


## <span id="ddk_opening_a_window_dbg"></span><span id="DDK_OPENING_A_WINDOW_DBG"></span>


WinDbg はデバッグ セッションを開始すると、[デバッガー コマンド ウィンドウ](debugger-command-window.md)が自動的に開きます。 [逆アセンブル ウィンドウ](disassembly-window.md)も自動的に開き、オフにしない限り[自動的に開く [逆アセンブル]](window---automatically-open-disassembly.md)上、**ウィンドウ**メニュー。

WinDbg に現在のプログラム カウンターに対応するソース ファイルが検出されるたびに WinDbg が表示されます、[ソース ウィンドウ](source-window.md)ファイル。 ソース ウィンドウを開くには、他の方法を参照してください。[ソース パス](source-path.md)します。

これらのウィンドウに切り替えるには、次のメニュー コマンド、ツール バー ボタン、およびショートカット キーを使用できます。 つまり、ウィンドウが開いていない場合が開きます。 ウィンドウが開きますが、非アクティブの場合は、アクティブになります。 ウィンドウのドッキングしフローティング ウィンドウに、先頭には、ドッキングされたウィンドウがアクティブになりますが、フローティング ウィンドウがドッキングされたウィンドウの手前に表示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Window</th>
<th align="left">メニュー コマンド</th>
<th align="left">Button</th>
<th align="left">ショートカット キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debugger-command-window.md" data-raw-source="[Debugger Command window](debugger-command-window.md)">デバッガー コマンド ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |コマンド</strong></p></td>
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Debugger Command window button" /></td>
<td align="left"><p>ALT + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>監視ウィンドウ</p></td>
<td align="left"><p><strong>ビュー |ウォッチ</strong></p></td>
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>ALT + 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locals-window.md" data-raw-source="[Locals window](locals-window.md)">[ローカル] ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |[ローカル]</strong></p></td>
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>ALT + 3</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="registers-window.md" data-raw-source="[Registers window](registers-window.md)">[レジスタ] ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |レジスタ</strong></p></td>
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>ALT + 4</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-window.md" data-raw-source="[Memory window](memory-window.md)">[メモリ] ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |メモリ</strong></p></td>
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>ALT + 5</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="calls-window.md" data-raw-source="[Calls window](calls-window.md)">コール スタック ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |呼び出し履歴</strong></p></td>
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>ALT + 6</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disassembly-window.md" data-raw-source="[Disassembly window](disassembly-window.md)">逆アセンブル ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |逆アセンブリ</strong></p></td>
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>ALT + 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>スクラッチ パッド ウィンドウ</p></td>
<td align="left"><p><strong>ビュー |スクラッチ パッド</strong></p></td>
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>ALT + 8</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="processes-and-threads-window.md" data-raw-source="[Processes and Threads window](processes-and-threads-window.md)">プロセスとスレッド ウィンドウ</a></p></td>
<td align="left"><p><strong>ビュー |プロセスとスレッド</strong></p></td>
<td align="left"><img src="images/window-processes-threads.png" alt="Screen shot of the Processes and Threads button" /></td>
<td align="left"><p>ALT + 9</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="source-window.md" data-raw-source="[Source window](source-window.md)">ソース ウィンドウ</a></p></td>
<td align="left"><p>クリックして<a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">ファイル |ソース ファイルを開く</a>し、ソース ファイルを選択します。</p></td>
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>Ctrl + O</p></td>
</tr>
</tbody>
</table>

 

選択してから、ウィンドウをアクティブ化することもできます、[開いているウィンドウのリスト](list-of-open-windows.md)の下部にある、**ウィンドウ**メニュー。

 

 





