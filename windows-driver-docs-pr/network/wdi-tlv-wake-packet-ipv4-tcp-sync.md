---
title: WDI_TLV_WAKE_PACKET_IPv4_TCP_SYNC
description: WDI_TLV_WAKE_PACKET_IPv4_TCP_SYNC では、wake on LAN IPv4 TCP 同期パケット情報を含む TLV です。
ms.assetid: C1237747-721C-4E44-B2BA-1B93E81174A8
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_IPv4_TCP_SYNC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b2cf053aa39a45614166145fdbe021520e5e93e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339951"
---
# <a name="wditlvwakepacketipv4tcpsync"></a>WDI\_TLV\_WAKE\_パケット\_IPv4\_TCP\_同期


WDI\_TLV\_WAKE\_パケット\_IPv4\_TCP\_同期は、wake on LAN IPv4 TCP 同期パケット情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x5D

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型       | 説明                                                      |
|------------|------------------------------------------------------------------|
| UINT32     | Wake on LAN のパターンの ID を指定します                            |
| UINT8\[4\] | TCP SYN パケットでは、IPv4 の発信元アドレスを指定します。         |
| UINT8\[4\] | TCP SYN パケットの IPv4 送信先アドレスを指定します。    |
| UINT16     | TCP SYN パケットでは、元の TCP ポート番号を指定します。      |
| UINT16     | TCP SYN パケットの宛先の TCP ポート番号を指定します。 |

 

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

 

 




