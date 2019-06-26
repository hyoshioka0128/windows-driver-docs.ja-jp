---
title: DVD 4 3 16 9 内でのパンのスキャン画像の例
description: DVD 4 3 16 9 内でのパンのスキャン画像の例
ms.assetid: f00489e7-809d-4a5b-87c8-b2421bd6ca93
keywords:
- アルファ ブレンドの組み合わせ WDK DirectX VA DVD 4 3 のパンのスキャンの例
- ブレンド画像 WDK DirectX va なので、DVD 4 3 パン スキャンの使用例
- DVD 4 3 パン スキャン例 WDK DirectX VA
- 4 3 パン スキャン例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db68850ce8afcf35c65a23c0f5c62976f2eb9708
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366803"
---
# <a name="dvd-43-pan-scan-within-169-pictures-example"></a>16:9 画像内での DVD 4:3 パン スキャンの例


## <span id="ddk_dvd_4_3_pan_scan_within_16_9_pictures_example_gg"></span><span id="DDK_DVD_4_3_PAN_SCAN_WITHIN_16_9_PICTURES_EXAMPLE_GG"></span>


4:3 パン スキャンは 16:9 のピクチャ内の mpeg-2 の使用を DVD、パン スキャン mpeg-2 変数する必要がありますに違反していないで指定された制限、 [ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)構造体。 これらの変数には、DVD 仕様で必要な次の制限も管理しなければなりません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Mpeg-2 変数</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>horizontal_size</em></p></td>
<td align="left"><p>720 または 704</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>vertical_size</em></p></td>
<td align="left"><p>480 または 576</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>display_horizontal_size</em></p></td>
<td align="left"><p>540</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>display_vertical_size</em></p></td>
<td align="left"><p><em>vertical_size</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>frame_centre_vertical_offset</em></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>frame_centre_horizontal_offset</em></p></td>
<td align="left"><p>以下の 1440 <em>horizontal_size</em> 720 を =</p>
<p>以下の 1312 に<em>horizontal_size</em> 704 を =</p></td>
</tr>
</tbody>
</table>

 

説明されている、定式化[mpeg-2 パン スキャン例](mpeg-2-pan-scan-example.md)適用できます。 直接この場合。

 

 





