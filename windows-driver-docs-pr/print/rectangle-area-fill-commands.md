---
title: 長方形領域塗りつぶしコマンド
description: 長方形領域塗りつぶしコマンド
ms.assetid: b9401126-4173-4187-960a-dc5ce69d3522
keywords:
- 四角形の領域の塗りつぶしの WDK Unidrv コマンドします。
- WDK Unidrv 長方形の領域を入力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a1ab975584a559681ac350097641ba20b0bdc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570589"
---
# <a name="rectangle-area-fill-commands"></a>長方形領域塗りつぶしコマンド





次の表は、四角形領域の塗りつぶしのコマンドを一覧表示します。 すべてのコマンドを使用して指定[コマンド エントリ形式](command-entry-format.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CmdRectBlackFill</p></td>
<td><p>黒のコマンドは、四角形を入力します。</p></td>
<td><p>任意。 指定しない場合、Unidrv がグレーの割合で CmdRectGrayFill コマンドを指定することで黒い塗りつぶしを試みます * MaxGrayFill します。</p></td>
</tr>
<tr class="even">
<td><p>CmdRectGrayFill</p></td>
<td><p>灰色のコマンドは、四角形を入力します。 (背景は消去されません)。</p></td>
<td><p>任意。 指定しない場合、Unidrv は灰色の塗りつぶしの機能を負いません。 コマンド文字列には、通常、GrayPercentage 変数が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p>CmdRectWhiteFill</p></td>
<td><p>白のコマンドは、四角形を入力します。 (背景を消去します。)</p></td>
<td><p>任意。 指定しない場合、Unidrv は消去白を負いません。 Unidrv の場合も、アプリケーション エラーが返されますことで、灰色の塗りつぶしがバック グラウンドを消去できないため、白の塗りつぶしを要求します。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectHeight</p></td>
<td><p>四角形の高さを設定するコマンドです。</p></td>
<td><p>任意。 必要があります、CmdSetRectWidth が指定されているかどうかに指定します。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetRectSize</p></td>
<td><p>四角形の幅と高さを設定するコマンドです。</p>
<p>Windows 2000 またはそれ以降、サポートされていません。</p></td>
<td><p>任意。 プリンター用に 1 つのコマンドで、幅と高さを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectWidth</p></td>
<td><p>四角形の幅を設定するコマンドです。</p></td>
<td><p>任意。 必要があります、CmdSetRectHeight が指定されているかどうかに指定します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




