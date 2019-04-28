---
title: WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC
description: WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC では、wake on LAN IPv6 TCP 同期パケット情報を含む TLV です。
ms.assetid: CBC0EA08-FDB4-415B-948C-E906F0471AD2
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1569cbbf9ec150d963961045a00724ff9b8a6814
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382136"
---
# <a name="wditlvwakepacketipv6tcpsync"></a>WDI\_TLV\_WAKE\_パケット\_IPv6\_TCP\_同期


WDI\_TLV\_WAKE\_パケット\_IPv6\_TCP\_同期は、wake on LAN IPv6 TCP 同期パケット情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x5E

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型        | 説明                                                      |
|-------------|------------------------------------------------------------------|
| UINT32      | WoL パターンの ID を指定します                                    |
| UINT8\[16\] | TCP SYN パケットの IPv6 送信元アドレスを指定します。         |
| UINT8\[16\] | TCP SYN パケットの IPv6 宛先アドレスを指定します。    |
| UINT16      | TCP SYN パケットでは、元の TCP ポート番号を指定します。      |
| UINT16      | TCP SYN パケットの宛先の TCP ポート番号を指定します。 |

 

<a name="requirements"></a>要件
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

 

 




