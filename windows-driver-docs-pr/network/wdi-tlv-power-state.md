---
title: WDI_TLV_POWER_STATE
description: WDI_TLV_POWER_STATE では、電源状態を含む TLV です。
ms.assetid: EC65FE08-ABF0-488A-A6FA-21B1794418B3
ms.date: 07/18/2017
keywords:
- WDI_TLV_POWER_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1f1b24240693da7075c8a90ebc5dc4986e79cfe4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342230"
---
# <a name="wditlvpowerstate"></a>WDI\_TLV\_POWER\_状態


WDI\_TLV\_POWER\_状態は、電源状態を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x44

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>電源の状態を指定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li>0x0001:省電力 (D0) の終了します。</li>
<li>0x0003:省電力 (D2) を入力します。</li>
<li>0x0004:オフ、電源を入力します (D3、可能性がありますいない実際に電源がオフで一部のプラットフォーム)</li>
</ul></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




