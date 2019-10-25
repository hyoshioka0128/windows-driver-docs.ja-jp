---
title: 色属性
description: 色属性
ms.assetid: c8de0186-9cf5-43e5-81e7-33351a34c13c
keywords:
- 色属性 WDK Unidrv
- 一般的なプリンター属性 WDK Unidrv、color
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f03b273275be2d1c5374ab8970b0e80881d94a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837981"
---
# <a name="color-attributes"></a>色属性





カラー属性は、カラー印刷を制御する特性を指定する[一般的な印刷属性](general-printing-attributes.md)です。

次の表に、カラー属性の一覧を示します。

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
<td><p><strong><em>ChangeColorModeOnDoc ですか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。 プリンターのカラーモードを、副作用なしでドキュメントのページ間で変更できるかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>TRUE</strong>になります。 Unidrv は、この値を使用して印刷速度を最適化します。 詳細については、この表の後の注を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>CyanInMagentaDye</strong></p></td>
<td><p>0 ~ 1000 の数値。これは、マゼンタ昇華のシアンの汚れの割合を示します。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CyanInYellowDye</strong></p></td>
<td><p>0 ~ 1000 の数値。黄色の昇華におけるシアンの汚れの割合を示します。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EnableGDIColorMapping</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。 GDI がプリンターの色空間に対して色域マッピングを実行する必要があるかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。 <strong>TRUE</strong>の場合、Unidrv は<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)"><strong>GDIINFO</strong></a>構造体の HT_FLAG_DO_DEVCLR_XFORM フラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MagentaInCyanDye</strong></p></td>
<td><p>シアン昇華のマゼンタ汚れの割合を示す 0 ~ 1000 の数値。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MagentaInYellowDye</strong></p></td>
<td><p>0 ~ 1000 の数値。黄色の昇華におけるマゼンタの汚れの割合を示します。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YellowInCyanDye</strong></p></td>
<td><p>シアン昇華の黄色の汚れの割合を示す 0 ~ 1000 の数値。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YellowInMagentaDye</strong></p></td>
<td><p>0 ~ 1000 の数値。マゼンタ昇華の黄色の汚れの割合を示します。 値は、100回目の汚れの割合を示します。 たとえば、8.4% の汚れは840として指定され、10% は1000になります。</p></td>
<td><p>(省略可能)。 指定しない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
</tbody>
</table>

 

**注**   **\*ChangeColorModeOnDoc?** color 属性が**TRUE**に設定されている場合、色の最適化が有効になります。 この属性が**FALSE**に設定されている場合、最適化は実行されません。 色の最適化が有効になっている場合、スプールファイルに色があると、スプールファイルが色で再生されます。スプールファイルに色がないと、スプールファイルがモノクロで再生されます。
カラーウォーターマークを生成するために Unidrv レンダリングプラグインを作成する場合は、白黒のドキュメントを印刷するときに色の透かしが白黒で印刷されることをお勧めします。 カラーウォーターマークが色と白黒のドキュメントで正しく印刷されるようにするには、色の最適化を無効にします。

**\*ChangeColorModeOnDoc?** color 属性によって制御される色の最適化は、[**属性\_INFO\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_2)または Attribute の**dwcoloroptimization**メンバーを設定することによって制御することもでき[ **\_INFO\_3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_3)の構造体。 色の最適化は、 [**GdiEndPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)関数を使用して制御することもできます。

 

このページに示されている色属性の例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




