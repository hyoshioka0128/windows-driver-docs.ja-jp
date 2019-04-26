---
title: 入力バッファー順序の例 6
description: 入力バッファー順序の例 6
ms.assetid: e94ca05a-5089-460a-bf71-ee6d8cf52f17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c60fba42711eab5e330641883c50582846aa9033
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350242"
---
# <a name="input-buffer-order-example-6"></a>入力バッファー順序の例 6


## <span id="ddk_input_buffer_order_example_6_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_6_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

前の 2 つの出力フレーム、旧バージョンとの参照を 1 つのサンプル、今後の参照を 1 つのサンプル、およびインター操作を実行する現在のサンプルが必要なより高度なインター デバイスを検討してください。 2 つのビデオ サブストリームはインター操作にも結合されます。 内のサーフェスのシーケンス、 **lpBufferInfo**配列。

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
<td align="left"><p>前の変換先</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>前の変換先</p></td>
<td align="left"><p>T-2</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[5]</p></td>
<td align="left"><p>インター レースの入力</p></td>
<td align="left"><p>T は + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[6]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[7]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

 

 





