---
title: PaperSize 機能のオプション属性
description: PaperSize 機能のオプション属性
ms.assetid: cfd82bc5-b89b-41c2-b542-28cb5905e37a
keywords:
- PaperSize 機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0358299ed31d7f114da95cc7c0b56609ee3c5178
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353694"
---
# <a name="option-attributes-for-the-papersize-feature"></a>PaperSize 機能のオプション属性





次の表は、PaperSize 機能に関連付けられている属性を一覧表示します。 PaperSize 機能の詳細については、次を参照してください。[標準機能](standard-features.md)します。

**注**  ランドス ケープなどのさまざまな方向を記述する属性を使用している場合でも、縦向きを基準とした、次の属性のすべての用紙サイズの仕様を表現する必要があります。

 

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
<td><p><em><strong>BottomMargin</strong></p></td>
<td><p>マスター CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズの単位の x で、許容される最小の下余白を表す数値を指定します。 値は、物理ページの下部にあります。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は 0 です。 CUSTOMSIZE オプションでのみ使用します。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CenterPrintable でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>の値を指定しているかどうかを示す<em> <strong>MaxPrintableWidth</strong>中央揃えで配置します。</p></td>
<td><p>(省略可能)。 印刷可能領域がで指定された余白の右側に指定しない場合、 <em> <strong>MinLeftMargin</strong>します。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CursorOrigin</strong></p></td>
<td><p>配信元のカーソル位置、マスター ユニットは、位置 (0, 0) のペアは、左上隅を表す数値の値のペア。 または、CUSTOMSIZE を使用してこれらの値を指定<em> <strong>CustCursorOriginX</strong>と *<strong>CustCursorOriginY</strong>します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は、(0, 0) のペアです。 Unidrv では、カーソル配信元のプリンターを基準とは異なる用紙サイズの定数を前提としています。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustCursorOriginX</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式でのインデックスの x 値を作成するために使用<em> <strong>CursorOrigin</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustCursorOriginY</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式でのインデックスの y 値を作成するために使用<em> <strong>CursorOrigin</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableOriginX</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式でのインデックスの x 値を作成するために使用<em> <strong>PrintableOrigin</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableOriginY</strong></p></td>
<td><p>CUSTOMSIZE パラメーター式でのインデックスの y 値を作成するために使用<em> <strong>PrintableOrigin</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CustPrintableSizeX</strong></p></td>
<td><p>X 値の値の作成に使用される、CUSTOMSIZE パラメーター式<em> <strong>PrintableArea</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>CustPrintableSizeY</strong></p></td>
<td><p>Y 値の値の作成に使用される、CUSTOMSIZE パラメーター式<em> <strong>PrintableArea</strong>します。</p></td>
<td><p>(省略可能)。 CUSTOMSIZE オプションでのみ使用します。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>最大サイズ</strong></p></td>
<td><p>ページの最大許容長さ (x) を表す数値と CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズのマスターの単位での高さ (y) の値のペア。</p></td>
<td><p>CUSTOMSIZE オプションが必要です。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxPrintableWidth</strong></p></td>
<td><p>X の最大印刷可能な幅を表す数値の値はマスター CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズの単位です。</p></td>
<td><p>CUSTOMSIZE オプションが必要です。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinLeftMargin</strong></p></td>
<td><p>マスター CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズの単位の最小許容左のマージンの x を表す数値を指定します。 物理的なページの左端からの相対値は、します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は 0 です。 CUSTOMSIZE オプションでのみ使用します。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MinSize</strong></p></td>
<td><p>許容されるページの最小の長さ (x) を表す数値と CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズのマスターの単位での高さ (y) の値のペア。</p></td>
<td><p>CUSTOMSIZE オプションが必要です。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PageDimensions</strong></p></td>
<td><p>ページの長さ (x) を表す数値とのいずれかのマスター単位の高さ (y) の値のペアは、用紙サイズ、機能のオプションをカスタマイズします。</p></td>
<td><p>ベンダー定義用紙サイズにのみ使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PageProtectMem</strong></p></td>
<td><p>ページを保護するために必要なキロバイト単位でのプリンター メモリの量を表す数値。</p></td>
<td><p>PageProtect 機能が指定されているかどうかに必要です。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintableArea</strong></p></td>
<td><p>X と y 平面、マスターの単位の長さ、印刷可能ページ領域を表す数値の値のペア。</p></td>
<td><p>CUSTOMSIZE を除くすべての用紙サイズ オプションで必要です。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintableOrigin</strong></p></td>
<td><p>用紙の左上隅を基準とした、マスターの単位での印刷可能領域の原点を表す数値の値のペア。</p></td>
<td><p>CUSTOMSIZE を除くすべての用紙サイズ オプションで必要です。 CUSTOMSIZE を使用してこれらの値を指定できます *<strong>CustPrintableOriginX</strong>と *<strong>CustPrintableOriginY</strong>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateSize でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>、(通常はエンベロープ) 給紙が横であるためにディメンション Unidrv、ページのローテーションが必要かどうかを示します。</p></td>
<td><p>(省略可能)。 指定されていない場合、既定値は<strong>FALSE</strong>します。 CUSTOMSIZE を除く、PaperSize 機能の任意の標準オプションで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TopMargin</strong></p></td>
<td><p>最小許容上余白、CUSTOMSIZE オプションに関連付けられているユーザーが指定した用紙サイズの y のマスターの単位を表す数値。 値は、物理的なページの先頭からの相対です。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は 0 です。 CUSTOMSIZE オプションでのみ使用します。 縦向きが使用されます。 参照してください<a href="specifying-paper-sizes.md" data-raw-source="[Specifying Paper Sizes](specifying-paper-sizes.md)">用紙サイズを指定する</a>します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

### <a href="" id="ddk-customsize-parameter-expressions-gg"></a>パラメーターの式を CUSTOMSIZE します。

カスタマイズ パラメーターの式は、制限付き形式の[コマンド文字列の形式](command-string-format.md)します。 テキスト文字列を指定することはできません。

式の内**型**セグメントでは、次の制限が適用されます。

-   唯一**型**指定できる値は %d です。

-   かっこで囲まれた値の範囲を指定することはできません。

式の内**StandardVariableExpression**セグメントでは、次の制限が適用されます。

-   PhysPaperWidth と PhysPaperLength 標準変数のみを使用できます。

-   **最大\_繰り返します**演算子は使用できません。

式の例を次に示します。

```cpp
*CustCursorOriginX: %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY: %d{180}
*CustPrintableOriginX: %d{300}
*CustPrintableOriginY: %d{300}
*CustPrintableSizeX: %d{PhysPaperWidth-600}
*CustPrintableSizeY: %d{PhysPaperLength-600}
```

 

 




