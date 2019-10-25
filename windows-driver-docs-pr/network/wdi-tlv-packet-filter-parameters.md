---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS は、OID_WDI_SET_RECEIVE_PACKET_FILTER のパケットフィルターパラメーターを含む TLV です。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- WDI_TLV_PACKET_FILTER_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ce40386c62c02bf00f302aaaeb14ac4e414fd86d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845151"
---
# <a name="wdi_tlv_packet_filter_parameters"></a>WDI\_TLV\_パケット\_フィルター\_パラメーター


WDI\_TLV\_パケット\_フィルター\_パラメーターは、OID\_WDI\_\_のパケットフィルターパラメーターを含む TLV です。このフィルターは、[受信\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-packet-filter)にます。

## <a name="tlv-type"></a>TLV 型


0x47

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                      | 説明                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_PACKET\_FILTER\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_packet_filter_type)(UINT32) | 目的の Wi-fi パケットフィルターを指定します。 |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




