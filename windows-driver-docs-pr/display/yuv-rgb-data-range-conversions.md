---
title: YUV-RGB データ範囲の変換
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 期待されるビデオ変換動作に対する入力データ範囲の影響
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d39a7325bdab737e251096e4043e6cfd31cdb82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829124"
---
# <a name="span-iddisplayyuv-rgb_data_range_conversionsspanyuv-rgb-data-range-conversions"></a><span id="display.yuv-rgb_data_range_conversions"></span>YUV-RGB データ範囲変換


RGB または YUV 入力から YUV または RGB 出力に変換する場合、期待される動作は入力データ範囲によって異なります。

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
<td align="left">データ</td>
<td align="left">format</td>
<td align="left">RGB</td>
<td align="left">基準</td>
<td align="left">RGB</td>
<td align="left">基準</td>
<td align="left">format</td>
<td align="left">データ</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">範囲</td>
<td align="left"></td>
<td align="left">範囲</td>
<td align="left">範囲</td>
<td align="left">範囲</td>
<td align="left">範囲</td>
<td align="left"></td>
<td align="left">範囲</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">なし</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">Scale</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">Scale</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">該当なし</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">該当なし</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">該当なし</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">該当なし</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">該当なし</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

この場合、"公称範囲" は、 [**DXVAHDDDI\_公称\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)列挙の定数値です。

YUV 形式の範囲の定義については[、「Windows 8.1 の yuv 形式の範囲](yuv-format-ranges.md)」を参照してください。

 

 





