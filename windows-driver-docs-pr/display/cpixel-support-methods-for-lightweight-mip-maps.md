---
title: 軽量の MIP マップ用の CPixel サポート メソッド
description: 軽量の MIP マップ用の CPixel サポート メソッド
ms.assetid: 79204a0c-c3a8-4059-a1be-9febf20a8cbd
keywords:
- 説明の CPixel インターフェイス
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 486b44e50e122a7b3e6ac16b471d366d5516c0eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574916"
---
# <a name="cpixel-support-methods-for-lightweight-mip-maps"></a>軽量の MIP マップ用の CPixel サポート メソッド


## <span id="ddk_cpixel_support_methods_for_lightweight_mip_maps_gg"></span><span id="DDK_CPIXEL_SUPPORT_METHODS_FOR_LIGHTWEIGHT_MIP_MAPS_GG"></span>


このセクションに定義されたメソッドを説明します、 **CPixel**クラス。 これらのメソッドは、軽量なシステム メモリの MIP マップ テクスチャのレイアウトを回復に使用されます。 メソッドのプロトタイプがで定義されている、 *pixel.hpp*ファイル。 このファイルと共に*pixel.cpp*と*pixlib.cpp*当初 Microsoft Windows ドライバー開発キット (DDK) に含まれ、作成に使用される、 *PixLib.lib*ライブラリをサポートします。 (前に、DDK、Windows Driver Kit \[WDK\])。

詳細については、 *PixLib.lib*ライブラリを参照してください、 [PixLib](https://go.microsoft.com/fwlink/p/?linkid=256156)ハードウェア デベロッパー センターのサンプル。

使用するように、ドライバーの**CPixel**クラスのメソッドに含める必要がありますが、 *pixel.hpp* 、コード内のファイルし、リンクする*PixLib.lib*ドライバーをビルドするとき。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CPixel クラスのメソッド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfacesize.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](cpixel-computesurfacesize.md)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>サーフェスの割り当てに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computevolumesize.md" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](cpixel-computevolumesize.md)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>ボリュームを割り当てるに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapsize.md" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](cpixel-computemipmapsize.md)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャを割り当てるために必要なメモリの量を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumesize.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](cpixel-computemipvolumesize.md)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャのボリュームを割り当てるに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computemipmapoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](cpixel-computemipmapoffset.md)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャのサブレベルのオフセットを決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="cpixel-computemipvolumeoffset.md" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](cpixel-computemipvolumeoffset.md)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>ボリュームの MIP マップ テクスチャの subvolume オフセットを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpixel-computesurfaceoffset.md" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](cpixel-computesurfaceoffset.md)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>サーフェスの subrectangular オフセットを決定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





