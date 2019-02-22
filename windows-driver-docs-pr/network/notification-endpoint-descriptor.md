---
title: 通知エンドポイント記述子
description: 通知エンドポイント記述子
ms.assetid: de15c698-a4a6-49f9-9faf-b9a64fe8b1c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72f6fd0fac0e2b012cb3216f5ea03eb5b6efa646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560858"
---
# <a name="notification-endpoint-descriptor"></a>通知エンドポイント記述子





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
<td align="left"><p>0x81</p></td>
<td align="left"><p>エンドポイント 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>エンドポイントを中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>wMaxPacketSize</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0008</p></td>
<td align="left"><p>8 バイトのパケットの最大サイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterval</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>ポーリング間隔</p></td>
</tr>
</tbody>
</table>

 

 

 





