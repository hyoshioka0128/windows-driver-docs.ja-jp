---
title: 入力バッファー順序の例 5
description: 入力バッファー順序の例 5
ms.assetid: f0ba80bb-ff84-4944-aae5-52eb0848edf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f61909e55eaf370fffe958f70998ea9eac8ce59b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350248"
---
# <a name="input-buffer-order-example-5"></a>入力バッファー順序の例 5


## <span id="ddk_input_buffer_order_example_5_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_5_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR ドライバーへの呼び出しを開始する[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)でデバイスを使用する関数[入力バッファーの順序の例 4](input-buffer-order-example-4.md)で 2 つのビデオ サブストリームを結合する、プログレッシブ ビデオ ストリーム。 これらのサンプルをコピー先のバッファーに出力を生成するために必要ない場合でも、VMR はまだプログレッシブ ビデオ サンプルのと同じ数を渡します。 内のサーフェスのシーケンス、 **lpBufferInfo**配列。

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
<td align="left"><p>プログレッシブの入力</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>プログレッシブの入力</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>プログレッシブの入力</p></td>
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

 

ドライバーは、インター操作に必要ではないために、インデックス 1 および 3 をインデックスにあるサーフェスを無視できます。 プログレッシブのサンプルは、DXVA でマークされた\_SampleProgressiveFrame フラグ、 **SampleFormat**のメンバー [ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)サンプルは、構造体。 サブストリームのサンプルは、新しい DXVA でマークされた\_SampleSubStream フラグ。

 

 





