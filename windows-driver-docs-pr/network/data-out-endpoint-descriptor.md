---
title: エンドポイント記述子送信データ
description: エンドポイント記述子送信データ
ms.assetid: 59a001c8-3723-4549-80ed-28ea8901dd87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81edac6dd3a68e03b663b95b3d77a4a5fb422fee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532854"
---
# <a name="data-out-endpoint-descriptor"></a>エンドポイント記述子送信データ





<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x07</p></td>
<td align="left"><p>この記述子は、バイト単位のサイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x05</p></td>
<td align="left"><p>エンドポイント記述子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>bEndpointAddress</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>OUT エンドポイント 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>一括エンドポイント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>wMaxPacketSize</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0040</p></td>
<td align="left"><p>64 バイトのパケットの最大サイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterval</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
</tbody>
</table>

 

 

 





