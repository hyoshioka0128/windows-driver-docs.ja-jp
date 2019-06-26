---
title: WDI_TLV_INDICATION_WAKE_PACKET
description: WDI_TLV_INDICATION_WAKE_PACKET は、NDIS_STATUS_WDI_INDICATION_WAKE_REASON のウェイク アップ パケットを含む TLV です。 ウェイク アップの理由は、WDI_WAKE_REASON_CODE パケットが、状態は、WDI_TLV_INDICATION_WAKE_PACKET にカプセル化されたウェイク アップ パケットを含める必要があります。
ms.assetid: 3C566FED-4594-403F-93D4-1CA6F2F655F9
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_WAKE_PACKET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dd1dd12dd2fbbe85c4980a2c8370b674d6036767
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380760"
---
# <a name="wditlvindicationwakepacket"></a>WDI\_TLV\_INDICATION\_WAKE\_パケット


WDI\_TLV\_を示す値\_WAKE\_パケットがウェイク アップ パケットを含む TLV [NDIS\_状態\_WDI\_INDICATION\_WAKE\_理由](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-wake-reason)します。 ウェイク アップの理由が WDI が場合\_WAKE\_理由\_コード パケットの場合、状態は、WDI にカプセル化されたウェイク アップ パケットを含める必要があります\_TLV\_INDICATION\_WAKE\_パケット。

## <a name="tlv-type"></a>TLV 型


0x9D

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                       |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | ウェイク アップ パケットです。 サイズは、パスを受信する、標準で示されるパケットのフラットなメモリのバージョンのサイズ。 |

 

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

 

 




