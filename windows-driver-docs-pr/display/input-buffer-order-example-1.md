---
title: 入力バッファー順序の例 1
description: 入力バッファー順序の例 1
ms.assetid: 1fd5f181-8bf7-4b16-adc9-ed751f9ad664
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5121bc7c489dceb4a4d6679c5c6fb88676d1f5d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350256"
---
# <a name="input-buffer-order-example-1"></a>入力バッファー順序の例 1


## <span id="ddk_input_buffer_order_example_1_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_1_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

任意の出力参照の前のフレームまたはデインター レース、操作を実行する前または将来の入力参照フレームを必要としないデバイスを検討してください (たとえば、 [deinterlacer を bob](bob-deinterlacing.md))。 における surface のシーケンス、 **lpBufferInfo**このデバイスの配列。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックスの位置</th>
<th align="left">画面の種類</th>
<th align="left">一時的な場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo [0]</p></td>
<td align="left"><p>宛先</p></td>
<td align="left"><p>T</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [1]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

 

 

 





