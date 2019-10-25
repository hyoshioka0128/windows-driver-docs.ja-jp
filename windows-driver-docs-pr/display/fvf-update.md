---
title: FVF 更新
description: FVF 更新
ms.assetid: 2bbcb1fd-b29f-41f4-93eb-5bd1cde9cb20
keywords:
- FVF WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a45cf4a887f1d649332fb7d152dc5c0a15067f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838935"
---
# <a name="fvf-update"></a>FVF 更新


## <span id="ddk_fvf_update_gg"></span><span id="DDK_FVF_UPDATE_GG"></span>


DirectX 6.0 でもともと定義されていた FVF コードは、DirectX 7.0 のテクスチャ座標セットの仕様をサポートするようになりました。

Directx 6.0 でサポートされている通常の2D テクスチャに加えて、DirectX 7.0 では、1D、3D、および4D テクスチャをサポートしています。 また、テクスチャが投影されることもあります。 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)の**Dwvertextype**メンバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)が呼び出されたときに調べることができます。これにより、各テクスチャ座標セットの次元が決定されます。

たとえば、5つのテクスチャ座標セットを持つ頂点がある場合、これらのテクスチャはそれぞれ1D、2D、3D、または4D で、テクスチャを投影することができます。 各テクスチャステージは独立しているため、座標のセットごとにディメンションが異なる場合があります。 **Dwvertextype**に含まれる FVF フラグの上位16ビットを調べて、テクスチャ座標の大きさを判断できます。

テクスチャ座標の数は、0 ~ 8 の範囲の4ビットフィールドです。 これにより、単語の上位16ビットで指定されたテクスチャ座標セットの数が示されます。 [FVF](fvf--flexible-vertex-format-.md)コードの上位16ビットは、8つのテクスチャ座標セットそれぞれに対して2つのビットとして割り当てられます。 テクスチャ座標ビットの意味は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bit
<div>
 
</div>
パターン</th>
<th align="left">Decimal
<div>
 
</div>
値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>2次元のテクスチャ座標ペア (u, v) は DirectX 6.0 のようになります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>01</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>3次元のテクスチャ座標三重、(u, v, q)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>4次元のテクスチャ座標4、(u、v、w、q)</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1次元のテクスチャ座標 (u)</p></td>
</tr>
</tbody>
</table>

 

3D テクスチャの座標セットは、射影されたテクスチャ (\_D3DTTFF によって通知されます)、ボリュームテクスチャ、または決定したように、キューブマップベクターテクスチャを3つの異なる目的のいずれかに使用できますテクスチャ座標セットに対して既に指定されている D3DRENDERSTATE\_WRAP0 to D3DRENDERSTATE\_WRAP7 モードに似た一連のレンダリング状態。

D3DRENDERSTATE\_と共に使用されるフラグは、次の表に示すように、1D によって 1D*のレンダリング状態*を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_0</p></td>
<td align="left"><p>D3DWRAP_U と同じ。 <em>U</em>座標方向での折り返しを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_1</p></td>
<td align="left"><p>D3DWRAP_V と同じ。 <em>V</em>座標方向での折り返しを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_2</p></td>
<td align="left"><p><em>W</em>座標方向での折り返しを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_3</p></td>
<td align="left"><p><em>Q</em>座標方向での折り返しを指定します。</p></td>
</tr>
</tbody>
</table>

 

投影されたテクスチャが使用中の場合、位置フィールドからではなく、対応するテクスチャ座標フィールドから RHW 値を取得します。 ただし、位置フィールドの RHW は、w バッファリングとフォグ計算の両方に使用されるため、これらのいずれかを使用するときに指定する必要があります。

 

 





