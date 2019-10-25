---
title: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0xDD)
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS は、IPv6 の Rx チェックサムオフロード用にを含む TLV です。
ms.assetid: F647B2B6-F535-4AE2-B7A9-DF08AADB2A95
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0xDD) ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 7eeb6416eeda52541839d8cf4aad98d8ee1b853f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841640"
---
# <a name="wdi_tlv_checksum_offload_v6_rx_parameters-0xdd"></a>WDI\_TLV\_CHECKSUM\_オフロード\_V6\_RX\_パラメーター (0xDD)


WDI\_TLV\_CHECKSUM\_オフロード\_V6\_RX\_パラメーターは、IPv6 の Rx チェックサムオフロード用にを含む TLV です。

機能の値は、「 [**NDIS\_TCP\_IP\_CHECKSUM\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)」に記載されているように報告されます。 \_サポートされておらず、NDIS\_オフロード\_を使用します。\_、 [OID\_WDI\_GET\_ADAPTER\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を使用して機能を指定する場合にサポートされ\_。

## <a name="tlv-type"></a>TLV 型


0xDD

## <a name="length"></a>Length


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>カプセル化の種類。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>IP 拡張ヘッダーのあるパケットのチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>TCP オプションを使用したチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>TCP チェックサムオフロードが有効かどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>UDP オフロードを有効にするかどうかを指定します。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




