---
title: デバイス記述子
description: デバイス記述子
ms.assetid: 5c533053-6a4e-4c28-a87d-562791298d5c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3720bfadfd468f2e2a040f5dbfaabbf54b168d62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551919"
---
# <a name="device-descriptor"></a>デバイス記述子





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
<td align="left"><p>0x12</p></td>
<td align="left"><p>この記述子は、バイト単位のサイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>デバイス記述子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>bcdUSB</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0110</p></td>
<td align="left"><p>1.1 - USB 仕様の現在のリビジョン</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bDeviceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>通信デバイス クラス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bDeviceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bDeviceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bMaxPacketSize0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x08</p></td>
<td align="left"><p>コントロールのパイプで最大パケット サイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>idVendor</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>ベンダ ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>idProduct</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>製品 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>bcdDevice</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0xXXXX</p></td>
<td align="left"><p>デバイス リリース コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14</p></td>
<td align="left"><p>iManufacturer</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>製造元の文字列のインデックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>15</p></td>
<td align="left"><p>iProduct</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>製品の文字列のインデックス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>iSerialNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>デバイスのシリアル番号の文字列のインデックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>bNumConfigurations</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>1 つの構成</p></td>
</tr>
</tbody>
</table>

 

 

 





