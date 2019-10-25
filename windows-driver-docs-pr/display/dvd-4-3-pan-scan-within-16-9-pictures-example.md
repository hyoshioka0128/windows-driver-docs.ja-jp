---
title: 16 9 画像内の DVD 4 3 パンスキャンの例
description: 16 9 画像内の DVD 4 3 パンスキャンの例
ms.assetid: f00489e7-809d-4a5b-87c8-b2421bd6ca93
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、DVD 4 3 のパンスキャンの例
- 画像のブレンド WDK DirectX VA、DVD 4 3 のパンスキャンの例
- DVD 4 3 パンスキャンの例 WDK DirectX VA
- 4 3 のパンスキャンの例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 754224a5cf1fddb52e42412a8f8647ae5611014b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838980"
---
# <a name="dvd-43-pan-scan-within-169-pictures-example"></a>16:9 画像内での DVD 4:3 パン スキャンの例


## <span id="ddk_dvd_4_3_pan_scan_within_16_9_pictures_example_gg"></span><span id="DDK_DVD_4_3_PAN_SCAN_WITHIN_16_9_PICTURES_EXAMPLE_GG"></span>


16:9 画像内で4:3 パンスキャンのために MPEG-2 を使用する DVD では、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体で指定された制限に、パンスキャン mpeg 2 変数が違反していてはなりません。 これらの変数は、DVD 仕様に必要な次の制限も保持する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MPEG-2 変数</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>horizontal_size</em></p></td>
<td align="left"><p>720または704</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>vertical_size</em></p></td>
<td align="left"><p>480または576</p></td>
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
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>frame_centre_horizontal_offset</em></p></td>
<td align="left"><p><em>Horizontal_size</em>の1440以下 = 720</p>
<p><em>Horizontal_size</em>の1312以下 = 704</p></td>
</tr>
</tbody>
</table>

 

この場合、 [MPEG-2 パンスキャンの例](mpeg-2-pan-scan-example.md)で説明されている定式化を直接適用できます。

 

 





