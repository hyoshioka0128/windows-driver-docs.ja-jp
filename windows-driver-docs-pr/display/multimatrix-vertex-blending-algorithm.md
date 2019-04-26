---
title: マルチマトリックス頂点ブレンド アルゴリズム
description: マルチマトリックス頂点ブレンド アルゴリズム
ms.assetid: 78ea0a92-a026-4c8d-a0ff-8be17b0a6424
keywords:
- 複数の行列による頂点の WDK の Direct3D をブレンディング アルゴリズム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6588bb880f2bca199fc33e9f27c001e0c6c7d32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345652"
---
# <a name="multimatrix-vertex-blending-algorithm"></a>マルチマトリックス頂点ブレンド アルゴリズム


## <span id="ddk_multimatrix_vertex_blending_algorithm_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_ALGORITHM_GG"></span>


ブレンディング アルゴリズムの複数の行列による頂点は、のみの 2 つの行列が使用されていることを前提としています。

マトリックスの変更時に、次の 4 つの行列を更新します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マトリックス</th>
<th align="left">計算</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>現在の変換行列 (CTM)</p></td>
<td align="left"><p>CTM = WORLD * VIEW * PROJ</p></td>
</tr>
<tr class="even">
<td align="left"><p>セカンダリ CTM (親の座標)</p></td>
<td align="left"><p>CTM2 = WORLD1 * VIEW * PROJ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTM の逆の転置</p></td>
<td align="left"><p>ITCTM = (CTM<sup>T</sup>) ⁻¹</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTM2 (光の場合に必要) の逆の転置</p></td>
<td align="left"><p>ITCTM2 = (CTM2<sup>T</sup>) ⁻¹</p></td>
</tr>
</tbody>
</table>

 

場合によっては、頂点の重みを使用してマトリックスを blend し、1 つだけ (matrix)X(vertex) 乗算の操作を実行する方が効率的場合があります。

 

 





