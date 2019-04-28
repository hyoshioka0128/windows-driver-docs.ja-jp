---
title: YUV-RGB データ範囲の変換
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 入力データの範囲の予期されるビデオの変換の動作への影響
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6022ff07872ee15099e8d4f96674eed88ec540b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371472"
---
# <a name="span-iddisplayyuv-rgbdatarangeconversionsspanyuv-rgb-data-range-conversions"></a><span id="display.yuv-rgb_data_range_conversions"></span>YUV RGB データ範囲の変換


YUV または RGB の出力に入力を RGB または YUV から変換する場合は、想定される動作は、入力データの範囲によって異なります。

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入力</th>
<th align="left">入力</th>
<th align="left">入力</th>
<th align="left">入力</th>
<th align="left">出力</th>
<th align="left">出力</th>
<th align="left">出力</th>
<th align="left">出力</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">data</td>
<td align="left">format</td>
<td align="left">RGB</td>
<td align="left">標準</td>
<td align="left">RGB</td>
<td align="left">標準</td>
<td align="left">format</td>
<td align="left">data</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">範囲 (range)</td>
<td align="left"></td>
<td align="left">範囲 (range)</td>
<td align="left">範囲 (range)</td>
<td align="left">範囲 (range)</td>
<td align="left">範囲 (range)</td>
<td align="left"></td>
<td align="left">範囲 (range)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">なし</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">Scale</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">Scale</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">なし</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">なし</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">なし</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">なし</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">なし</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

定数値を"標準"範囲がここでは、 [ **DXVAHDDDI\_公称\_範囲**](https://msdn.microsoft.com/library/windows/hardware/dn265432)列挙体。

参照してください[YUV 形式の範囲の Windows 8.1 で](yuv-format-ranges.md)YUV の定義については、範囲をフォーマットします。

 

 





