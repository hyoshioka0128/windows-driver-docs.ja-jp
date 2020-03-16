---
title: PaperSize 機能のオプション属性
description: PaperSize 機能のオプション属性
ms.assetid: cfd82bc5-b89b-41c2-b542-28cb5905e37a
keywords:
- 用紙の機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0358299ed31d7f114da95cc7c0b56609ee3c5178
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242909"
---
# <a name="option-attributes-for-the-papersize-feature"></a>PaperSize 機能のオプション属性





次の表に、PaperSize 機能に関連付けられている属性を示します。 PaperSize 機能の詳細については、「[標準機能](standard-features.md)」を参照してください。

**注**   次の属性の用紙サイズの指定はすべて、横などのさまざまな向きを示すために使用されている場合でも、縦向きを基準にして表す必要があります。

 

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
<td><p><em>下<strong>余白</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズについて、許容される最小の下限 (x マスター単位) を表す数値。 値は、物理ページの下部に対する相対値です。</p></td>
<td><p>省略可。 値を指定しない場合は、既定値 0 が使用されます。 CUSTOMSIZE オプションと共にのみ使用されます。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>センターに印刷しますか?</strong></p></td>
<td><p><em><strong>Maxprintablewidth</strong>によって指定された値を中央揃えにするかどうかを示す<strong>TRUE</strong>または<strong>FALSE</strong>。</p></td>
<td><p>省略可。 指定しない場合、印刷可能な領域は <em><strong>MinLeftMargin</strong>によって指定された余白の右側になります。 CUSTOMSIZE オプションと共にのみ使用されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>カーソルオリジン</strong> を </em><strong></p></td>
<td><p>カーソルの原点の位置を表す数値のペア (マスター単位)。ここで、PAIR (0, 0) は左上隅にあります。 または、CUSTOMSIZE に対して、<em><strong>Custカーソルの原点 x</strong>と *<strong>Custカーソルの原点</strong>を使用して、これらの値を指定します。</p></td>
<td><p>省略可。 指定しない場合、既定値は PAIR (0, 0) になります。 Unidrv は、プリンターを基準としたカーソルの原点を、用紙サイズが異なる定数であると想定しています。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Custカーソルの原点 x</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>カーソルオリジン</strong>の x インデックスの値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Custカーソルの原点 y</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>カーソルオリジン</strong>の y インデックスの値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Custprintable原点 x</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>Printableorigin</strong>の x インデックスの値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Custprintabley</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>Printableorigin</strong>の y インデックスの値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableSizeX</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>Printablearea</strong>の x 値の値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableSizeY</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式。 <em><strong>Printablearea</strong>の y 値の値を作成するために使用されます。</p></td>
<td><p>省略可。 CUSTOMSIZE オプションと共にのみ使用してください。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxSize</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズに対して許容される最大ページ長 (x) 値と高さ (y) 値をマスター単位で表す数値のペア。</p></td>
<td><p>CUSTOMSIZE オプションに必要です。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Maxprintablewidth</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズの印刷可能な最大幅を x マスター単位で表す数値。</p></td>
<td><p>CUSTOMSIZE オプションに必要です。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinLeftMargin</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズについて、許容される最小の左余白 (x マスター単位) を表す数値。 値は、物理ページの左端からの相対値です。</p></td>
<td><p>省略可。 値を指定しない場合は、既定値 0 が使用されます。 CUSTOMSIZE オプションと共にのみ使用されます。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MinSize</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズについて、許容される最小ページ長 (x) 値と高さ (y) 値をマスター単位で表す数値のペア。</p></td>
<td><p>CUSTOMSIZE オプションに必要です。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PageDimensions</strong></p></td>
<td><p>ページ長 (x) と高さ (y) の値をマスター単位で表す数値のペアで、用紙の機能のカスタマイズされたオプションを指定します。</p></td>
<td><p>ベンダー定義の用紙サイズにのみ使用されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PageProtectMem</strong></p></td>
<td><p>ページの保護に必要なプリンターメモリの量 (kb 単位) を表す数値。</p></td>
<td><p>PageProtect 機能が指定されている場合は必須です。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintableArea</strong></p></td>
<td><p>印刷可能なページ領域の x および y 平面の長さをマスター単位で表す数値のペア。</p></td>
<td><p>CUSTOMSIZE を除くすべての PaperSize オプションに必要です。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Printableorigin</strong></p></td>
<td><p>用紙の左上隅を基準とした、印刷可能領域の原点 (マスター単位) を表す数値のペア。</p></td>
<td><p>CUSTOMSIZE を除くすべての PaperSize オプションに必要です。 CUSTOMSIZE の場合、これらの値は、*<strong>Custprintable原点 x</strong>と *<strong>Custprintable原点 y</strong>を使用して指定できます。</p></td>
</tr>
<tr class="even">
<td><p>RotateSize を </em><strong>しますか?</strong></p></td>
<td><p>用紙 (通常は封筒) が横向きに給紙されるため、Unidrv がページのサイズを回転させるかどうかを示す<strong>TRUE</strong>または<strong>FALSE</strong>。</p></td>
<td><p>省略可。 指定しない場合、既定値は<strong>FALSE</strong>になります。 は、CUSTOMSIZE を除く、PaperSize 機能の任意の標準オプションと共に使用できます。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TopMargin</strong></p></td>
<td><p>CUSTOMSIZE オプションに関連付けられているユーザー指定の用紙サイズについて、許容される最小の上余白 (y マスター単位) を表す数値。 値は、物理ページの上端からの相対値です。</p></td>
<td><p>省略可。 値を指定しない場合は、既定値 0 が使用されます。 CUSTOMSIZE オプションと共にのみ使用されます。 縦向きが想定されます。 「<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズの指定」を</a>参照してください。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

### <a href="" id="ddk-customsize-parameter-expressions-gg"></a>CUSTOMSIZE パラメーター式

パラメーター式のカスタマイズは、制限された形式の[コマンド文字列形式](command-string-format.md)です。 文字列は使用できません。

式の**Argumenttype**セグメント内では、次の制限が適用されます。

-   使用できる**Argumenttype**値は% d のみです。

-   角かっこで囲まれた値の範囲は使用できません。

式の**Standard変数 expression**セグメント内では、次の制限が適用されます。

-   使用できるのは、PhysPaperWidth と PhysPaperLength の標準変数だけです。

-   **Max\_Repeat**演算子は使用できません。

式の例を次に示します。

```cpp
*CustCursorOriginX: %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY: %d{180}
*CustPrintableOriginX: %d{300}
*CustPrintableOriginY: %d{300}
*CustPrintableSizeX: %d{PhysPaperWidth-600}
*CustPrintableSizeY: %d{PhysPaperLength-600}
```

 

 




