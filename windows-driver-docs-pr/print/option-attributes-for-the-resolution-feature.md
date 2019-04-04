---
title: Resolution 機能のオプション属性
description: Resolution 機能のオプション属性
ms.assetid: f04cd119-38c7-465c-b4fd-d657aa5bfacd
keywords:
- 解決の機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bebafb031a2958c7e09c5baf3396d4d175f051a2
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349923"
---
# <a name="option-attributes-for-the-resolution-feature"></a>Resolution 機能のオプション属性





次の表は、解決の機能に関連付けられている属性を一覧表示します。 解決策機能の詳細については、[標準機能](standard-features.md)を参照してください。

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
<td><p><em><strong>DPI</strong></p></td>
<td><p>X を表す数値とプリンターの解像度、インチあたりのドットでの y 値のペア。</p></td>
<td><p>必須。 X および y 値を等しく必要があります *<strong>TextDPI</strong> x と y 値、またはそれらが等しくする必要があります *<strong>TextDPI</strong> x と y の値が 2 の累乗で割った値します。 たとえば場合、*<strong>TextDPI</strong>し (300、300) のペアは、*<strong>DPI</strong>ペア (300、300)、ペア (150, 150)、または (75, 75) のペアがないペア (100, 100) を値として使用することがあります。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinStripBlankPixels</strong></p></td>
<td><p>空白は、外側の空白のバイトを削除する前に、スキャン ライン内 Unidrv が発生する必要があります (バイト) の最小数を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。 この属性は、関連する場合にのみ、 <em> <strong>StripBlanks</strong> ENCLOSED を指定します。 参照してください<a href="raster-data-emission-attributes.md" data-raw-source="[Raster Data Emission Attributes](raster-data-emission-attributes.md)">ラスター データ出力属性</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PinsPerLogPass</strong></p></td>
<td><p>スキャンの印刷ヘッドの 1 つの論理パスによって出力される行数を表示する数値。 倍数である必要があります<em> <strong>PinsPerPhysPass</strong>、ため各論理パスは、1 つまたは複数の物理パスで構成されています。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。 インター レース、一連のすべてのスキャン ラインを印刷する、スキャン ラインの印刷ヘッドの複数のパスを必要とするかどうか、プリンターを実行しますが必要です。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PinsPerPhysPass</strong></p></td>
<td><p>印刷ヘッドが、ページ間で移動すると、スキャン ラインの数を表す数値が印刷されます。 1 つ、または 8 の倍数である必要があります。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。</p>
<p>水平および垂直方向の解像度の倍数である必要があります<em> <strong>PinsPerPhysPass</strong>、または出力が予測可能な可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RequireUniDir でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示すかどうか指定の解像度が一方向の印刷を有効にする必要があります。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>SpotDiameter</strong></p></td>
<td><p>指定された解決のため、ピクセル サイズの割合としてスポットの直径のサイズを表す数値を指定 *<strong>DPI</strong>します。</p></td>
<td><p>必須。</p>
<p>例:</p>
100 では、スポット直径ピクセル サイズに等しいことを意味します。
200 は、スポット直径がピクセル サイズの 2 倍を意味します。
スポットの直径がピクセルの半分のサイズを 50 に意味します。</td>
</tr>
<tr class="odd">
<td><p></em><strong>TextDPI</strong></p></td>
<td><p>ペアまたは数値を表す x と y 値の 1 インチあたりのドット数で、プリンターのテキストの解決。</p></td>
<td><p>必須。 参照してください *<strong>DPI</strong>コメント。 この解決は、フォントおよびベクター グラフィックスを描画するために使用されます。</p></td>
</tr>
</tbody>
</table>

 

例については、、[サンプル GPD ファイル](sample-gpd-files.md)を参照してください。

追加のオプションの属性については、[すべての機能のオプション属性](option-attributes-for-all-features.md)を参照してください。

参照してください[画質を制御する](controlling-image-quality.md)します。

 

 




