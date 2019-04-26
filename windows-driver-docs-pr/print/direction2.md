---
title: Direction
description: Direction
ms.assetid: 19aa1c88-968d-4789-89cc-00b76b1a30d9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128f89fd1fabbd08524d3adf634292aa9a5346d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342838"
---
# <a name="direction"></a>Direction


スキーマのパス:\\Printer.Layout.NumberUp.Direction

ノード型: プロパティ

説明: メディア上の複数の論理ページの配置の順序を決定するプロパティ。 このプロパティの子の値には、現在の方向と印刷デバイスでサポートされている手順の一覧が含まれます。

Direction プロパティには、2 つの子の値が含まれています。CurrentValue サポートされているとします。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

スキーマのパス:\\Printer.Layout.NumberUp.Direction:CurrentValue

ノード型: 値

データ型: BIDI\_文字列

説明: 現在の論理ページをレイアウトするための (既定値) の向き。 それぞれの値は、水平方向と垂直方向で構成されます。

次の表では、使用可能な値を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
<th>論理ページの順序 (4Up)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RightDown</p></td>
<td><p>行、シートの一番上の最初の行に内の論理ページに印刷され、シートの低い印刷行を指します。 各の行では、右から左への論理ページが印刷されます。</p></td>
<td><p>2 1</p>
<p>4 3</p></td>
</tr>
<tr class="even">
<td><p>DownRight</p></td>
<td><p>最初の列に、シートの右側にある最も近いで縦の列内の論理ページを印刷し、遠くの列を指す、シート上の残りします。 各列内での論理ページが上から下に印刷されます。</p></td>
<td><p>3 1</p>
<p>4 2</p></td>
</tr>
<tr class="odd">
<td><p>LeftDown</p></td>
<td><p>行、シートの一番上の最初の行に内の論理ページに印刷され、シートの低い印刷行を指します。 行ごとに、内の論理ページが左から右に印刷されます。</p></td>
<td><p>1 2</p>
<p>3 4</p></td>
</tr>
<tr class="even">
<td><p>DownLeft</p></td>
<td><p>シート上よりも右に、シートの左側にある最も近いの最初の列を使用して垂直列と続く列内の論理ページを印刷します。 各列内での論理ページが上から下に印刷されます。</p></td>
<td><p>1 3</p>
<p>2 4</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> サポートされています

スキーマのパス:\\Printer.Layout.NumberUp.Direction:Supported

ノード型: 値

データ型: BIDI\_文字列

説明: A 方向でサポートされているすべての値のコンマ区切り一覧。

 

 




