---
title: FVF 更新
description: FVF 更新
ms.assetid: 2bbcb1fd-b29f-41f4-93eb-5bd1cde9cb20
keywords:
- FVF WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66f04e47f76ccd00df6c8c06bbab5f6336092cad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383439"
---
# <a name="fvf-update"></a>FVF 更新


## <span id="ddk_fvf_update_gg"></span><span id="DDK_FVF_UPDATE_GG"></span>


FVF コード最初に定義された DirectX 6.0 ようになりました DirectX 7.0 でのテクスチャ座標のセットの仕様。

だけでなく、通常 2 D テクスチャ、DirectX 6.0、7.0 を DirectX サポート 1 D、3 D、および 4 D のテクスチャではサポートされています。 さらに、テクスチャを投影することがあります。 **DwVertexType**のメンバー [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)ときに検査できる[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)各テクスチャの座標セットのサイズを調べるために呼び出されます。

たとえば、5 つのテクスチャ座標のセットでの頂点がある場合これらのテクスチャのそれぞれが 1 次元、2 D、3 D を指定できます。 または 4 D とそれらに、射影されたテクスチャを指定することがあります。 ディメンションを座標のセットごとに異なることができるように、各テクスチャ ステージは独立しており、です。 含まれている FVF フラグの上位 16 ビット**dwVertexType**テクスチャ座標の大きさを調べることができます。

テクスチャ座標の数は、4 ビット 0 から 8 までの範囲のことができます。 これにより、単語の上位 16 ビットで指定されたテクスチャ座標のセットの数。 上位 16 ビット、 [FVF](fvf--flexible-vertex-format-.md)ごとに 8 つのテクスチャ座標のセットの各ビットを 2 つと、コードが割り当てられます。 テクスチャ座標のビットの意味は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット
<div>
 
</div>
[パターン]</th>
<th align="left">10 進数
<div>
 
</div>
Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>2 次元テクスチャ DirectX 6.0 のようにのペア、(u、v) を調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>01</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>3 次元テクスチャ座標 triple (u、v、q)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>4 次元テクスチャ座標の 4 倍、(u、v、w、q)</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1 次元テクスチャ座標、u</p></td>
</tr>
</tbody>
</table>

 

次の 3 つのさまざまな目的のいずれかの 3D テクスチャ座標のセットを使用できます: テクスチャを投影 (D3DTTFF によって通知\_投影 - DirectX sdk で D3DTEXTURETRANSFORMFLAGS を参照してください)、ボリューム テクスチャ、そのキューブとして、ベクターにテクスチャをマップします。一連の描画状態、D3DRENDERSTATE に似ていますによって決まります\_D3DRENDERSTATE に WRAP0\_WRAP7 モード テクスチャで既に指定されているセットごとの調整。

D3DRENDERSTATE で使用するフラグ\_ラップ*n*レンダリングの状態 1 D 4 D のテクスチャ座標をそれぞれ、次の表に記載されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_0</p></td>
<td align="left"><p>D3DWRAP_U での折り返しを指定すると同じ、 <em>u</em>方向を調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_1</p></td>
<td align="left"><p>D3DWRAP_V での折り返しを指定すると同じ、 <em>v</em>方向を調整します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_2</p></td>
<td align="left"><p>折り返しを指定します、 <em>w</em>方向を調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_3</p></td>
<td align="left"><p>折り返しを指定します、 <em>q</em>方向を調整します。</p></td>
</tr>
</tbody>
</table>

 

投影されたテクスチャを使用しているときに、値を受け取り、RHW 対応するテクスチャ座標フィールドからの代わりに位置フィールドから。 ただし、位置フィールドの RHW が w バッファリングとフォグの計算の両方の使用され、したがって必要がありますを指定するときにこれらのいずれかが使用されます。

 

 





