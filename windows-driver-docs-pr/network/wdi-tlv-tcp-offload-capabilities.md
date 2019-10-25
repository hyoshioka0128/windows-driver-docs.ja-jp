---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES は、TCP/IP オフロード機能を含む TLV です。
ms.assetid: 9B3428CC-C9B4-4769-BD97-F25920C4AAF2
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_OFFLOAD_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: a44520bdf680456891f3f71f1a5eb1ddd4e93c2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841724"
---
# <a name="wdi_tlv_tcp_offload_capabilities"></a>WDI\_TLV\_TCP\_オフロード\_の機能


WDI\_TLV\_TCP\_オフロード\_機能は、TCP/IP オフロード機能を含む TLV です。

機能の値は、「 [**NDIS\_TCP\_IP\_CHECKSUM\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)」に記載されているように報告されます。 \_サポートされておらず、NDIS\_オフロード\_を使用します。\_、 [OID\_WDI\_GET\_ADAPTER\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を使用して機能を指定する場合にサポートされ\_。 FIPS モードの接続では、オフロードは UE-V によってオフにされます。

## <a name="tlv-type"></a>TLV 型


0xCA

## <a name="length"></a>長さ


含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                                                        | 複数の TLV インスタンスを使用できます | オプション | 説明                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_チェックサム\_オフロード\_の機能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | チェックサムオフロード機能。      |
| [**WDI\_TLV\_LSO\_V1\_機能**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大規模な送信オフロード V1 の機能。 |
| [**WDI\_TLV\_LSO\_V2\_の機能**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大規模な送信オフロード V2 の機能。 |
| [**WDI\_TLV\_\_の結合\_オフロード\_機能**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | 受信オフロード機能。       |
| [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) |   |   | オフロードが STA ポートのみに適用されるか、すべてのポートに適用されるかを示します。 現在は、802.11 ad アダプターにのみ適用されます。 |

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

 

 




