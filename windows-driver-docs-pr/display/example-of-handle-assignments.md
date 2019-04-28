---
title: ハンドル割り当ての例
description: ハンドル割り当ての例
ms.assetid: 44239e13-ebe7-48c4-83b2-40f603dc1c98
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0、ハンドルの割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3f708021d3e47b490be44fc2bf200f3f8bd991b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365941"
---
# <a name="example-of-handle-assignments"></a>ハンドル割り当ての例


## <span id="ddk_example_of_handle_assignments_gg"></span><span id="DDK_EXAMPLE_OF_HANDLE_ASSIGNMENTS_GG"></span>


次の表は、Direct3D のハンドル値の並べ替え方法の例を示します (を介して提供された[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)) ヘッドが 2 つのシナリオに存在する必要があります。 各ヘッドがすべてのフロント、バックと深度ステンシル/サーフェスがある一意のハンドル。これらのハンドルのすべての master head が動作する必要があります。 すべてのテクスチャ、頂点バッファー、およびインデックス バッファーのサーフェスを所有する master headこれらのサーフェスのハンドルは、master head でのみ作成されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Master head の値を処理します。</th>
<th align="left">下位の head の値を処理します。</th>
<th align="left">Surface</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"></td>
<td align="left"><p>マスターのフロント バッファー</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"></td>
<td align="left"><p>マスターのバック バッファー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"></td>
<td align="left"><p>マスターの深度バッファー</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>下位のフロント バッファー</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>下位のバック バッファー</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>下位の深度バッファー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"></td>
<td align="left"><p>マスターのテクスチャ 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"></td>
<td align="left"><p>マスターのテクスチャ 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"></td>
<td align="left"><p>マスターのテクスチャ 3</p></td>
</tr>
</tbody>
</table>

 

 

 





