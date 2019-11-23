---
title: ミニポート アダプター Direct OID 要求
description: ミニポート アダプター Direct OID 要求
ms.assetid: 63ced5a3-0c83-4952-aa0e-c3c654b3f241
keywords:
- 直接 OID 要求インターフェイス WDK ネットワーク
- 直接 OID 要求パス WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6226da35a5dfd99f66274685185bebf246c58524
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844253"
---
# <a name="miniport-adapter-direct-oid-requests"></a>ミニポート アダプター Direct OID 要求





直接 OID 要求パスをサポートするために、ミニポートドライバーは、 [**ndis\_ミニポート\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の*miniportxxx*関数のエントリポイントを提供します。また、\_特性の構造と NDIS は、ミニポートドライバー用の**ndism * Xxx*** 関数を提供します。

*直接 oid 要求インターフェイス*は、標準の oid 要求インターフェイスに似ています。 たとえば、 [**NdisMDirectOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete)関数と[*Miniportdirectoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request)関数は、 [**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)および[*miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数に似ています。

**注**  NDIS 6.1 では、直接 oid 要求インターフェイスで使用する特定の oid がサポートされています。 NDIS 6.1 および一部の NDIS 6.1 Oid より前に存在していた Oid はサポートされていません。 直接 oid インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。 

ミニポートドライバーは、シリアル化されていない直接 OID 要求を処理できる必要があります。 標準の OID 要求インターフェイスとは異なり、NDIS では直接 OID 要求を直接 oid インターフェイスまたは標準の OID 要求インターフェイスと共に送信される他の要求と共にシリアル化しません。 また、ポートドライバーは、IRQL &lt;= ディスパッチ\_レベルで直接 OID 要求を処理できる必要があります。

直接 Oid 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表は、直接 OID 要求インターフェイスの関数と標準の OID 要求インターフェイスの間の関係を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">直接 OID 関数</th>
<th align="left">標準 OID 関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)"><em>MiniportOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_direct_oid_request)"><em>Miniportcancelt Toidrequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)"><em>MiniportCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete)"><strong>NdisMDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





