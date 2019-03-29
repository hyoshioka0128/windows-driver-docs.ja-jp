---
title: WDI_TLV_WAKE_PACKET_MAGIC_PACKET
description: WDI_TLV_WAKE_PACKET_MAGIC_PACKET は、OID_WDI_SET_ADD_WOL_PATTERN のマジック パケットのパターンの ID を含む TLV です。
ms.assetid: F1DEB65B-8DD4-4D4A-9DCB-950C3B562F0A
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_MAGIC_PACKET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2f62b79a89d92e1158ffa8d21b71e96adafbed13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578341"
---
# <a name="wditlvwakepacketmagicpacket"></a>WDI\_TLV\_WAKE\_パケット\_マジック\_パケット


WDI\_TLV\_WAKE\_パケット\_マジック\_パケットがマジック パケットのパターンの ID を含む TLV [OID\_WDI\_設定\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/dn925858)します。

## <a name="tlv-type"></a>TLV 型


0x5C

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                        |
|--------|----------------------------------------------------|
| UINT32 | マジック パケットの wake on LAN のパターンの ID を指定します |

 

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

 

 




