---
title: 入力バッファー順序の例 4
description: 入力バッファー順序の例 4
ms.assetid: 56370370-4786-44e4-9447-3937e4595e27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69293f3be29a822eb087a62b41e3d1d0c0507d9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350224"
---
# <a name="input-buffer-order-example-4"></a>入力バッファー順序の例 4


## <span id="ddk_input_buffer_order_example_4_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_4_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

旧バージョンとの参照を 1 つのサンプルや今後の参照を 1 つのサンプルでは、現在のサンプルを実行するを必要とするより高度なデインター レース デバイスを検討してください。 その操作のインター レースを解除します。 2 つのビデオ サブストリームはインター操作にも結合されます。 内のサーフェスのシーケンス、 **lpBufferInfo**配列。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックスの位置</th>
<th align="left">画面の種類</th>
<th align="left">一時的な場所</th>
<th align="left">レイヤーの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo [0]</p></td>
<td align="left"><p>宛先</p></td>
<td align="left"><p>T</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [1]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T は + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[5]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

 

 





