---
title: 長方形領域塗りつぶし属性
description: 長方形領域塗りつぶし属性
ms.assetid: 287e8805-4aec-490b-88da-00576a2f4fbf
keywords:
- 四角形の領域の塗りつぶし属性 WDK Unidrv
- WDK Unidrv 長方形の領域を入力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 398503590d0714be0b7f9f80f480efa02d3406b3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349187"
---
# <a name="rectangle-area-fill-attributes"></a>長方形領域塗りつぶし属性





次の表は、四角形領域の塗りつぶしのプリンターのサポートを記述する属性を一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>CursorXAfterRectFill</strong></p></td>
<td><p>AT_RECT_X_ORIGIN または AT_RECT_X_END、プリンターが四角形領域を塗りつぶします後に、カーソルの x 座標の位置を示すです。</p></td>
<td><p>任意。 指定しない場合、既定値は AT_RECT_X_ORIGIN にします。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterRectFill</strong></p></td>
<td><p>AT_RECT_Y_ORIGIN または AT_RECT_Y_END、プリンターが四角形領域を塗りつぶします後に、カーソルの y 座標の位置を示すです。</p></td>
<td><p>任意。 指定しない場合、既定値は AT_RECT_Y_ORIGIN にします。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxGrayFill</strong></p></td>
<td><p>CmdRectGrayFill コマンドの引数として許可されているグレーの塗りつぶしの最大パーセンテージを表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 100 (パーセント) にします。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinGrayFill</strong></p></td>
<td><p>CmdRectGrayFill コマンドの引数として許可されている最小の灰色の塗りつぶしの割合を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 (%) にします。</p></td>
</tr>
</tbody>
</table>

 

プリンターの四角形領域の塗りつぶしの機能に関連付けられているコマンドについては、[四角形領域の塗りつぶしコマンド](rectangle-area-fill-commands.md)を参照してください。

例については、、[サンプル GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




