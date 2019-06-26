---
title: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0xDD)
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS では、IPv6 のチェックサムがオフロード Rx 用を含む TLV です。
ms.assetid: F647B2B6-F535-4AE2-B7A9-DF08AADB2A95
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0 xdd) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 169a55d0e77d955b07809e50d1fc879debb7b022
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387195"
---
# <a name="wditlvchecksumoffloadv6rxparameters-0xdd"></a>WDI\_TLV\_チェックサム\_オフロード\_V6\_RX\_パラメーター (0 xdd)


WDI\_TLV\_チェックサム\_オフロード\_V6\_RX\_パラメーターは、IPv6 の Rx チェックサム オフロード用を含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)します。

## <a name="tlv-type"></a>TLV 型


0 xdd を設定

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
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
<td>拡張機能の IP ヘッダーのあるパケットのチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>TCP オプションを使用してチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>TCP チェックサム オフロードが有効になっているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>UDP のオフロードが有効になっているかどうかを指定します。</td>
</tr>
</tbody>
</table>

 

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

 

 




