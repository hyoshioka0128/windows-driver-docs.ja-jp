---
title: 入力バッファー順序の例 2
description: 入力バッファー順序の例 2
ms.assetid: e480bd93-4ae2-4a6c-b669-69c44c0154d0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068b22606ac23dc27bf4ac4a5b5e29fcbe9b4499
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379928"
---
# <a name="input-buffer-order-example-2"></a>入力バッファー順序の例 2


## <span id="ddk_input_buffer_order_example_2_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_2_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR ドライバーへの呼び出しを開始する[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)でデバイスを使用する関数[入力バッファーの順序の例 1](input-buffer-order-example-1.md)インター レースと 2 つのビデオ サブストリームを結合するにはビデオ ストリーム。 内のサーフェスのシーケンス、 **lpBufferInfo**配列。

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
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

 

 





