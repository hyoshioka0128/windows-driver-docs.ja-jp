---
title: WDI_TLV_CHECKSUM_OFFLOAD_V4_RX_PARAMETERS (0xD2)
description: WDI_TLV_CHECKSUM_OFFLOAD_V4_RX_PARAMETERS は、IPv4 の Rx チェックサムオフロードのパラメーターを含む TLV です。
ms.assetid: A06E0534-CD5E-4D81-AEC8-CFC6106AAD85
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V4_RX_PARAMETERS (0xD2) ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 6ee2ab91e9c386fd22d699c34db6ece8330d5abe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841651"
---
# <a name="wdi_tlv_checksum_offload_v4_rx_parameters-0xd2"></a>WDI\_TLV\_CHECKSUM\_オフロード\_V4\_RX\_PARAMETERS (0xD2)


WDI\_TLV\_CHECKSUM\_オフロード\_V4\_RX\_PARAMETERS は、IPv4 の Rx チェックサムオフロードのパラメーターを含む TLV です。

機能の値は、「 [**NDIS\_TCP\_IP\_CHECKSUM\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)」に記載されているように報告されます。 \_サポートされておらず、NDIS\_オフロード\_を使用します。\_、 [OID\_WDI\_GET\_ADAPTER\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を使用して機能を指定する場合にサポートされ\_。

## <a name="tlv-type"></a>TLV 型


0xD2

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>カプセル化の設定。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>IP オプションを使用したチェックサムのオフロードがサポートされているかどうかを指定します。</td>
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
<tr class="even">
<td>UINT32</td>
<td>IP チェックサムを有効にするかどうかを指定します。</td>
</tr>
</tbody>
</table>

 

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

 

 




