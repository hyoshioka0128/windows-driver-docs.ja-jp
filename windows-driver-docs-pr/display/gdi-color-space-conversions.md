---
title: GDI 色空間の変換
description: GDI 色空間の変換
ms.assetid: f1840d58-9f93-4aa3-8344-d5e61c176254
keywords:
- セキュリティ ネゴシエーション WDK GDI、色空間の変換
- カラー チャネルの WDK GDI
- 色空間の変換が WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e48825a3262057b0ee189ea52f08fe451d0478a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559825"
---
# <a name="gdi-color-space-conversions"></a>GDI 色空間の変換


## <span id="ddk_gdi_color_space_conversions_gg"></span><span id="DDK_GDI_COLOR_SPACE_CONVERSIONS_GG"></span>


GDI は、そのビットマップ表現を次の 3 つの RGB 色空間を使用します。 これら 3 つのビット フィールドの色空間の各または*チャネルのカラー*赤、緑、青の特定の色で、それぞれに使用されるビット数を指定するために使用します。 ビットマップの GDI の機能を活用できるようにするには、ビデオ ドライバーは、1 つの RGB 色空間から別に変換できる必要があります。

GDI は、次の RGB 色空間を認識します。

-   5:5:5 RGB: 赤、緑、青の 5 ビット カラー チャネル

-   5:6:5 RGB: 赤、緑に 6 ビット カラー チャネル、および青の 5 ビット カラー チャネルの 5 ビット カラー チャネル

-   8:8:8 RGB: 赤、緑、青の 8 ビットのカラー チャネル

一般より多くのビットのカラー チャネルからビット数が少ないのいずれかへの変換、GDI は下位ビットを破棄します。 ビット数が少ないのカラー チャネルからのビット数を 1 つになると、変換のすべての小規模なチャネルのビットより大きなチャネルにコピーします。 大規模なチャネルの残りのビットを記入するには、一部の小規模なチャネルのビットもう一度チャネルにコピー、拡大します。 次の表では、GDI が 1 つの RGB 色空間からの変換に使用する規則をまとめたものです。 このテーブルで値を変更する変換でのカラー チャネルが示すように**太字**フォント スタイル。

### <a name="span-idgdicolorspaceconversionrulesspanspan-idgdicolorspaceconversionrulesspanspan-idgdicolorspaceconversionrulesspangdi-color-space-conversion-rules"></a><span id="GDI_Color_Space_Conversion_Rules"></span><span id="gdi_color_space_conversion_rules"></span><span id="GDI_COLOR_SPACE_CONVERSION_RULES"></span>GDI 色空間変換規則

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">移行元</th>
<th align="left">目的</th>
<th align="left">ルール</th>
<th align="left">例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>ソースの最上位ビット (MSB)&#39;s 緑チャネルは、ターゲットの下位の末尾に追加されます&#39;s 緑チャネル。</p></td>
<td align="left"><p>(0x15、 <strong>0x19</strong>0x1D) になります</p>
<div>
 
</div>
(0x15、 <strong>0x33</strong>0x1D)
<div>
 
</div>
緑チャネルの変更だけであるに注意してください。 ソースの 5 ビット チャネルの値は、1 1001、バイナリ、11 0011 6 ビット値に変換されます。</td>
</tr>
<tr class="even">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>チャネルごとに、ソース チャネルの 3 つ MSBs は対象のチャネルの下位の末尾に追加されます。</p></td>
<td align="left"><p>(<strong>0x15</strong>、 <strong>0x19</strong>、 <strong>0x1D</strong>) になります</p>
<div>
 
</div>
(<strong>0xAD</strong>、 <strong>0xCE</strong>、 <strong>0xEF</strong>)
<div>
 
</div>
赤チャネルで 1 0101 1010 1101 になります。 ような変更は、緑、青のチャネルで発生します。</td>
</tr>
<tr class="odd">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>破棄、ソースの最下位ビット (lsb に向かって)&#39;s 緑チャネル。</p></td>
<td align="left"><p>(0x15、 <strong>0x33</strong>0x1D) になります</p>
<div>
 
</div>
(0x15、 <strong>0x19</strong>0x1D)
<div>
 
</div>
緑チャネルの変更だけであるに注意してください。 最下位ビットを破棄します。
<div>
 
</div>
取得 1 1001 11 0011 します。</td>
</tr>
<tr class="even">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>ソースの 5 ビット (赤、青) チャネル、ソースからの 3 つの MSBs のコピーし、ターゲットの下位の末尾に追加します。 6 ビット緑チャネルの 2 つの MSBs をソースからコピーし、それらをターゲットの下位の末尾に追加します。</p></td>
<td align="left"><p>(<strong>0x15</strong>、 <strong>0x33</strong>、 <strong>0x1D</strong>) になります</p>
<div>
 
</div>
(<strong>0xAD</strong>、 <strong>0xCF</strong>、 <strong>0xEF</strong>)
<div>
 
</div>
赤チャネルで 1 0101 1010 1101 になります。 緑色のチャネルでは 11 0011 になります
<div>
 
</div>
1100 1111. 青のチャネルでの変換は、赤チャネルに似ています。</td>
</tr>
<tr class="odd">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>ソースの各チャネルから次の 3 つ LSBs を破棄します。</p></td>
<td align="left"><p>(<strong>0xAB</strong>、 <strong>0 xcd</strong>、 <strong>0xEF</strong>) になります</p>
<div>
 
</div>
(<strong>0x15</strong>、 <strong>0x19</strong>、 <strong>0x1D</strong>)
<div>
 
</div>
赤チャネル 1010 1011 1 0101 になります。 ような変換は、その他の 2 つのチャネルで発生します。</td>
</tr>
<tr class="even">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>赤、青のチャネルから次の 3 つ LSBs を破棄します。 緑チャネルからの 2 つの LSBs を破棄します。</p></td>
<td align="left"><p>(<strong>0xAB</strong>、 <strong>0 xcd</strong>、 <strong>0xEF</strong>) になります</p>
<div>
 
</div>
(<strong>0x15</strong>、 <strong>0x33</strong>、 <strong>0x1D</strong>)
<div>
 
</div>
緑色のチャネルで 1100 1101 11 0011 になります。 赤、青チャネルの変更が以前表示されている変換のと同じです。</td>
</tr>
</tbody>
</table>

 

 

 





