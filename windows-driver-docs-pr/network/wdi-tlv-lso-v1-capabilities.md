---
title: WDI_TLV_LSO_V1_CAPABILITIES (0xCC)
description: WDI_TLV_LSO_V1_CAPABILITIES は、大規模な送信オフロード V1 の機能を含む TLV です。
ms.assetid: 22C5778A-F551-4931-A19C-7AA399221B3D
ms.date: 07/18/2017
keywords:
- WDI_TLV_LSO_V1_CAPABILITIES (0xCC) ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 5d4724e07e305fb4d370d437948876992afabc2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842462"
---
# <a name="wdi_tlv_lso_v1_capabilities-0xcc"></a>WDI\_TLV\_LSO\_V1\_機能 (0xCC)


WDI\_TLV\_LSO\_V1\_機能は、大規模な送信オフロード V1 の機能を含む TLV です。

機能の値は、「 [**NDIS\_TCP\_IP\_CHECKSUM\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)」に記載されているように報告されます。 \_サポートされておらず、NDIS\_オフロード\_を使用します。\_、 [OID\_WDI\_GET\_ADAPTER\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を使用して機能を指定する場合にサポートされ\_。

## <a name="tlv-type"></a>TLV 型


0xCC

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
<td>カプセル化の種類。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大オフロードサイズ。 パケットあたりの TCP ユーザーデータの最大バイト数で指定されます。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>トランスポートがセグメント化のためにハードウェアにオフロードする前に、大きな TCP パケットが割り切れないセグメントの最小数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>このオフロードで TCP オプションをサポートするかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>このオフロードで IP オプションがサポートされているかどうかを指定します。</td>
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

 

 




