---
title: 入力バッファー順序の例 5
description: 入力バッファー順序の例 5
ms.assetid: f0ba80bb-ff84-4944-aae5-52eb0848edf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0297d8bc8c3f7948eea48652b295ffebdd53d7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840363"
---
# <a name="input-buffer-order-example-5"></a>入力バッファー順序の例 5


## <span id="ddk_input_buffer_order_example_5_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_5_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR は、ドライバーの[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数の呼び出しを開始して、[入力バッファーの順序例 4](input-buffer-order-example-4.md)のデバイスを使用し、2つのビデオサブストリームをプログレッシブビデオストリームと結合します。 このサンプルでは、出力先のバッファーに出力を生成する必要がない場合でも、VMR は同じ数のプログレッシブビデオサンプルを渡します。 **Lpbufferinfo**配列内の一連のサーフェイスは次のとおりです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス位置</th>
<th align="left">サーフェイスの種類</th>
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
<td align="left"><p>プログレッシブ入力</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>プログレッシブ入力</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [3]</p></td>
<td align="left"><p>プログレッシブ入力</p></td>
<td align="left"><p>T + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [5]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、ノンインターレース操作に必要ではないため、インデックス1とインデックス3のサーフェスを無視できます。 プログレッシブサンプルは、サンプルの[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**SAMPLEFORMAT**メンバーの DXVA\_SampleProgressiveFrame フラグでマークされています。 サブストリームのサンプルには、新しい DXVA\_SampleSubStream フラグが設定されています。

 

 





