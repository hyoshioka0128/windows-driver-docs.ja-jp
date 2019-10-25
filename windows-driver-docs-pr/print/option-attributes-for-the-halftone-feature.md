---
title: Halftone 機能のオプション属性
description: Halftone 機能のオプション属性
ms.assetid: a188908a-ddf7-4b4d-a46d-e3550ffb0418
keywords:
- ハーフトーン機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6a6f3813cfa045061ac9be072fd9a25ad6210c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843053"
---
# <a name="option-attributes-for-the-halftone-feature"></a>Halftone 機能のオプション属性





次の表に、ハーフトーン機能に関連付けられている属性を示します。 ハーフトーン機能の詳細については、「[標準機能](standard-features.md)」を参照してください。

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
<td><p><em><strong>Htの id</strong></p></td>
<td><p>表示プラグインの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)"><strong>Iprintoemuni:: HalftonePattern</strong></a>メソッドに<em>dwcallbackid</em>パラメーターとして渡される正の数値。</p></td>
<td><p><strong>Iprintoemuni:: HalftonePattern</strong>メソッドが指定されている場合は必須です。 「 <a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv によるハーフトーン」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>HTNumPatterns</strong></p></td>
<td><p>指定されたハーフトーンパターンの数を表す数値。</p>
<p>「 <a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv によるハーフトーン」を</a>参照してください。</p></td>
<td><p>(省略可能)。 1または3にすることができます。ここで、3は、赤、緑、および青の個別のパターンを示しています。 指定しない場合、既定値は1です。 は、<em><strong>rcHTPatternID</strong>または *<strong>ht id</strong>と共に使用できます。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Htpattern サイズ</strong></p></td>
<td><p><em><strong>rcHTPatternID</strong>で指定されたパターンの幅と高さをピクセル単位で表す数値の<a href="pairs.md" data-raw-source="[Pair](pairs.md)">ペア</a>。</p></td>
<td><p>*<strong>RcHTPatternID</strong>が指定されている場合は必須です。 最大パターンサイズはペア (256, 256) です。 Dword としてストレージを使用するには、幅と高さを乗算して4で割り切れる必要があります。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcHTPatternID</strong></p></td>
<td><p>ハーフトーンパターンデータを表す RC_HTPATTERN リソースのリソース識別子。</p></td>
<td><p>ハーフトーンパターンがリソース DLL に指定されている場合は必須です。 「 <a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv によるハーフトーン」を</a>参照してください。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

これらの属性の使用方法の詳細については、「 [Unidrv によるハーフトーン](halftoning-with-unidrv.md)」を参照してください。 これらの属性は[、ミニドライバーが提供するハーフトーン](minidriver-supplied-halftoning.md)では使用されません。

 

 




