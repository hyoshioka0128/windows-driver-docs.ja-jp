---
title: ツール バーとステータス バーの使用
description: ツール バーとステータス バーの使用
ms.assetid: 96427166-b6df-4f6b-b550-69d0eb33042d
keywords:
- ツールバー (WinDbg)
- ツールバー (WinDbg), 概要
- ボタン (WinDbg ツールバー)
- ボタン (WinDbg ツールバー), 概要
- ステータス バー
- ステータス バー、概要
- WinDbg, ツールバー
- WinDbg、ステータス バー
- WinDbg をボタン
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d95640ccb586e68ab50324107fa9ac298aa917
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340516"
---
# <a name="using-the-toolbar-and-status-bar"></a>ツール バーとステータス バーの使用


## <span id="ddk_using_the_toolbar_and_status_bar_dbg"></span><span id="DDK_USING_THE_TOOLBAR_AND_STATUS_BAR_DBG"></span>


*ツールバー* WinDbg ウィンドウの上部のメニュー バーの下に表示されます。 *ステータス バー* WinDbg ウィンドウの下部に表示されます。

### <a name="span-idusingthetoolbarspanspan-idusingthetoolbarspanusing-the-toolbar"></a><span id="using_the_toolbar"></span><span id="USING_THE_TOOLBAR"></span>ツールバーの使用

次のスクリーン ショットには、WinDbg ツールバーが表示されます。

![windbg のツールバーのスクリーン ショット](images/toolbar4.png)

ツール バー ボタンには、さまざまな影響があります。 これらのほとんどは、メニュー コマンドと同じです。 ツール バー ボタンに関連付けられているコマンドを実行するには、ツール バー ボタンをクリックします。 ボタンを使用できない場合は、使用できない表示されます。

各ボタンの詳細については、次を参照してください。[ツール バー ボタン](toolbar-buttons.md)します。

### <a name="span-idusingthestatusbarspanspan-idusingthestatusbarspanusing-the-status-bar"></a><span id="using_the_status_bar"></span><span id="USING_THE_STATUS_BAR"></span>ステータス バーを使用します。

次のスクリーン ショットには、WinDbg のステータス バーが表示されます。

![windbg のステータス バーのスクリーン ショット](images/statusbar3.png)

次の表では、WinDbg ステータス バーのセクションでは、について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">セクション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>メッセージ</p></td>
<td align="left"><p>デバッガーからのメッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ln、Col</p></td>
<td align="left"><p>アクティブなカーソルに行番号および列番号を表示します。<a href="source-window.md" data-raw-source="[Source window](source-window.md)">ソース ウィンドウ</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Sys</p></td>
<td align="left"><p>をデバッグしているシステムの内部の 10 進数の表示後にそのコンピューター名 (または<strong>&lt;ローカル&gt;</strong>デバッガーが実行されているコンピューターと同じである場合)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>proc</p></td>
<td align="left"><p>をデバッグしているプロセスの内部の 10 進数の表示後に 16 進数のプロセス ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Thrd</p></td>
<td align="left"><p>をデバッグしているスレッドの内部の 10 進数の表示後に 16 進数のスレッド ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>ASM</p></td>
<td align="left"><p>WinDbg がモードのアセンブリであることを示します。 ASM が使用可能な場合は、WinDbg はソース モードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>上書</p></td>
<td align="left"><p>上書きモードがアクティブなことを示します。 上書が使用可能な場合は、挿入モードがアクティブにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>キャップ</p></td>
<td align="left"><p>CAPS LOCK がであることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NUM</p></td>
<td align="left"><p>NUM LOCK がオンにすることを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhidingthetoolbarorstatusbarspanspan-idhidingthetoolbarorstatusbarspanhiding-the-toolbar-or-status-bar"></a><span id="hiding_the_toolbar_or_status_bar"></span><span id="HIDING_THE_TOOLBAR_OR_STATUS_BAR"></span>ツールバーやステータス バーを非表示

または、ツールバーを非表示には、オンまたはオフ[ツールバー](view---toolbar.md)上、**ビュー**メニュー。 または、ステータス バーを非表示には、オンまたはオフ[ステータス バー](view---status-bar.md)上、**ビュー**メニュー。

ツールバーやステータス バーを非表示にする場合、WinDbg で windows の表示領域の情報をデバッグするためのより多くの領域があります。

### <a name="span-idsettingthewindowtitlespanspan-idsettingthewindowtitlespansetting-the-window-title"></a><span id="setting_the_window_title"></span><span id="SETTING_THE_WINDOW_TITLE"></span>ウィンドウのタイトルを設定

使用して、WinDbg ウィンドウのタイトルを変更することができます、 [ **.wtitle (ウィンドウ タイトルの設定)** ](-wtitle--set-window-title-.md)コマンド。

 

 





