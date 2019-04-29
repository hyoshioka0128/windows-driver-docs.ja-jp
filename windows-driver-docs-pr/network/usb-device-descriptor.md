---
title: USB デバイス記述子
description: USB デバイス記述子
ms.assetid: ef2a3e43-0e55-4e8e-ad86-efcbe153c847
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c260bfbac83c4beea5f77ccbab097255a0a0b15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384978"
---
# <a name="usb-device-descriptor"></a>USB デバイス記述子





デバイスは、USB 仕様で定義されている USB デバイスの記述子を返します。 次の表では、USB デバイス記述子の著名なフィールドを定義します。

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
<th align="left">オフセット (バイト)</th>
<th align="left">フィールド</th>
<th align="left">サイズ (バイト)</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>bDeviceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
<td align="left"><p>デバイス クラスのコードを通信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>bDeviceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>通信デバイス サブクラス コード、この時点で使用されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>bDeviceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>通信デバイス プロトコル コード、この時点で使用されていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





