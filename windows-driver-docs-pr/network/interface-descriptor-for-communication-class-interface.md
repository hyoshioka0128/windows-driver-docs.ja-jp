---
title: クラスの通信インターフェイスのインターフェイスの記述子
description: クラスの通信インターフェイスのインターフェイスの記述子
ms.assetid: e3873a58-34fc-4ca0-8c45-197401cbf08b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87c6169d447e5d49e316d589045d5d96ad7e02d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550202"
---
# <a name="interface-descriptor-for-communication-class-interface"></a>クラスの通信インターフェイスのインターフェイスの記述子





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
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x04</p></td>
<td align="left"><p>インターフェイスの記述子</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>bInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>このインターフェイスのインデックス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>bAlternateSetting</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>この設定のインデックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bNumEndpoints</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>1 つのエンドポイント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>通信クラス</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubclass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>コントロールの抽象モデル</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0 xff の場合</p></td>
<td align="left"><p>ベンダー固有のプロトコル</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>iInterface</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
</tbody>
</table>

 

 

 





