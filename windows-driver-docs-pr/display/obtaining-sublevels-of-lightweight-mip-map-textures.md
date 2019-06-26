---
title: 軽量の MIP マップ テクスチャのサブレベルの取得
description: 軽量の MIP マップ テクスチャのサブレベルの取得
ms.assetid: a2781c9a-b4bb-42a9-8ed5-9f62c1d2ee64
keywords:
- MIP マップ テクスチャ WDK DirectX 9.0、サブレベルの取得
- 軽量の MIP マップ テクスチャ WDK DirectX 9.0、サブレベルの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd1ce4b0a5a3e89accb32b2a62695fdd61a9e068
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372782"
---
# <a name="obtaining-sublevels-of-lightweight-mip-map-textures"></a>軽量の MIP マップ テクスチャのサブレベルの取得


## <span id="ddk_obtaining_sublevels_of_lightweight_mip_map_textures_gg"></span><span id="DDK_OBTAINING_SUBLEVELS_OF_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


DirectX 9.0 バージョンのドライバーを使用して、 [CPixel クラスのメソッド](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-support-methods-for-lightweight-mip-maps)軽量の MIP マップ テクスチャの最上位レベルに関する唯一の情報を格納する軽量なシステム メモリの MIP マップ テクスチャ--の下位レベルのに関する情報を取得します。 ドライバーは、ビデオ メモリに軽量なシステム メモリの MIP マップ テクスチャをコピーする必要があります、ドライバーは、ソース テクスチャのサイズとソース テクスチャの下位レベルへのオフセットを計算するのに CPixel クラスのメソッドを使用できます。

ドライバーの作成者は、CPixel クラスのメソッドを使用して軽量の MIP マップ テクスチャの下位レベルの場所を計算する必要はありません。 ただし、DirectX 9.0 ランタイムを使用して**CPixel**クラスの軽量なシステム メモリの MIP マップ テクスチャのメモリ レイアウトを回復する方法。 そのため、ランタイムとドライバーが同様に、軽量なシステム メモリの MIP マップ テクスチャのメモリ レイアウトを回復することを確認するには、ドライバー作成者従う必要があります、同じ**CPixel**規則、独自のコードを実装するクラスします。

方法については**CPixel**クラスの実装を参照してください、 *pixel.hpp*、 *pixel.cpp*、および*pixlib.cpp* 内のファイル[PixLib](https://go.microsoft.com/fwlink/p/?linkid=256156)コード サンプル。

CPixel クラスには、次のメソッドが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CPixel メソッド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfacesize" data-raw-source="[&lt;strong&gt;ComputeSurfaceSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfacesize)"><strong>ComputeSurfaceSize</strong></a></p></td>
<td align="left"><p>サーフェスの割り当てに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computevolumesize" data-raw-source="[&lt;strong&gt;ComputeVolumeSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computevolumesize)"><strong>ComputeVolumeSize</strong></a></p></td>
<td align="left"><p>ボリュームを割り当てるに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapsize" data-raw-source="[&lt;strong&gt;ComputeMipMapSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapsize)"><strong>ComputeMipMapSize</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャを割り当てるために必要なメモリの量を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumesize" data-raw-source="[&lt;strong&gt;ComputeMipVolumeSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumesize)"><strong>ComputeMipVolumeSize</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャのボリュームを割り当てるに必要なメモリの量を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapoffset" data-raw-source="[&lt;strong&gt;ComputeMipMapOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipmapoffset)"><strong>ComputeMipMapOffset</strong></a></p></td>
<td align="left"><p>MIP マップ テクスチャのサブレベルのオフセットを決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumeoffset" data-raw-source="[&lt;strong&gt;ComputeMipVolumeOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computemipvolumeoffset)"><strong>ComputeMipVolumeOffset</strong></a></p></td>
<td align="left"><p>ボリュームの MIP マップ テクスチャの subvolume オフセットを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfaceoffset" data-raw-source="[&lt;strong&gt;ComputeSurfaceOffset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/cpixel-computesurfaceoffset)"><strong>ComputeSurfaceOffset</strong></a></p></td>
<td align="left"><p>サーフェスの subrectangular オフセットを決定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





