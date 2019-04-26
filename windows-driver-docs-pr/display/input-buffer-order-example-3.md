---
title: 入力バッファー順序の例 3
description: 入力バッファー順序の例 3
ms.assetid: 627102bb-e7a8-4b6d-9a52-f8bf4b9727d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ea1e3299ef37febc5e68ce9402e1d899cdbefc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350259"
---
# <a name="input-buffer-order-example-3"></a>入力バッファー順序の例 3


## <span id="ddk_input_buffer_order_example_3_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_3_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR ドライバーへの呼び出しを開始する*DeinterlaceBltEx*でデバイスを使用する関数[入力バッファーの順序の例 1](input-buffer-order-example-1.md)と[入力バッファーの使用例 2](input-buffer-order-example-2.md)を代わりに3 つのビデオ サブストリームをプログレッシブ ビデオ ストリームに組み合わせます。 内のサーフェスのシーケンス、 **lpBufferInfo**配列。

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
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>サブストリーム</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 3</p></td>
</tr>
</tbody>
</table>

 

2 ~ 3 個の例からの変更、プログレッシブにインター レースから変更されて、ビデオ ストリームとその他のビデオ サブストリームがアクティブになりました。

 

 





