---
title: ハーフトーン機能のオプションの属性
description: ハーフトーン機能のオプションの属性
ms.assetid: a188908a-ddf7-4b4d-a46d-e3550ffb0418
keywords:
- ハーフトーン機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c24b5a8f7c99bee149e0bf90be555553b568eb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551173"
---
# <a name="option-attributes-for-the-halftone-feature"></a>ハーフトーン機能のオプションの属性





次の表は、ハーフトーン機能に関連付けられている属性を一覧表示します。 ハーフトーン機能の詳細については、次を参照してください。[標準機能](standard-features.md)します。

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
<td><p><em><strong>HTCallbackID</strong></p></td>
<td><p>レンダリングに渡される正の数値がプラグイン&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff554258" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554258)"> <strong>IPrintOemUni::HalftonePattern</strong> </a>メソッドとしてその<em>dwCallbackID</em>パラメーター。</p></td>
<td><p>必要な場合、 <strong>IPrintOemUni::HalftonePattern</strong>メソッドが提供されます。 参照してください<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv のハーフトーン</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>HTNumPatterns</strong></p></td>
<td><p>ハーフトーン パターンの数を表す数値。</p>
<p>参照してください<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv のハーフトーン</a>します。</p></td>
<td><p>(省略可能)。 1 またはできます 3、3 は赤、緑、およびその順序で、青の個別のパターンを意味します。 指定しない場合、既定値は 1 です。 いずれかで使用できる<em> <strong>rcHTPatternID</strong>または *<strong>HTCallbackID</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>HTPatternSize</strong></p></td>
<td><p><a href="pairs.md" data-raw-source="[Pair](pairs.md)">ペア</a>幅と高さ (ピクセル単位) で指定されたパターンを表す数値の<em> <strong>rcHTPatternID</strong>します。</p></td>
<td><p>必要な場合 *<strong>rcHTPatternID</strong>を指定します。 パターンの最大サイズは、(256、256) のペアです。 幅と高さ、乗算を Dword 記憶域の 4 で割り切れる必要があります指定します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcHTPatternID</strong></p></td>
<td><p>ハーフトーン パターンのデータを表す RC_HTPATTERN リソースのリソース識別子です。</p></td>
<td><p>ハーフトーン パターンがリソース DLL で提供されているかどうかに必要です。 参照してください<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv のハーフトーン</a>します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

これらの属性の使用に関する詳細については、次を参照してください。 [Unidrv のハーフトーン](halftoning-with-unidrv.md)します。 これらの属性を使用しない[ミニドライバーが指定したハーフトーン](minidriver-supplied-halftoning.md)します。

 

 




