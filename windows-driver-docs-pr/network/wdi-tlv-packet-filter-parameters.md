---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS は、OID_WDI_SET_RECEIVE_PACKET_FILTER のパケット フィルター パラメーターを含む TLV です。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- WDI_TLV_PACKET_FILTER_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fefe392f204db6abb985054e2658573e2cf8886d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385411"
---
# <a name="wditlvpacketfilterparameters"></a>WDI\_TLV\_パケット\_フィルター\_パラメーター


WDI\_TLV\_パケット\_フィルター\_パラメーターは、のパケット フィルター パラメーターを含む TLV [OID\_WDI\_設定\_受信\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-packet-filter)します。

## <a name="tlv-type"></a>TLV 型


0x47

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型                                                                      | 説明                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_パケット\_フィルター\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_packet_filter_type) (UINT32) | 必要な Wi-fi パケット フィルターを指定します。 |

 

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

 

 




