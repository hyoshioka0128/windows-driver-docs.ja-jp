---
title: フィルター モジュール Direct OID 要求
description: フィルター モジュール Direct OID 要求
ms.assetid: 0ab7079b-6578-4932-a276-40a961b55efe
keywords:
- 直接 OID 要求インターフェイス WDK ネットワーク
- 直接 OID 要求パス WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd083d32602dc2eac5838e8be5182b999b3b230d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834688"
---
# <a name="filter-module-direct-oid-requests"></a>フィルター モジュール Direct OID 要求





直接 OID 要求パスをサポートするために、フィルタードライバーは、 [**ndis\_フィルター\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)の*filterxxx*関数のエントリポイントを提供します。\_特性の構造と NDIS は、フィルター用の**NdisF * Xxx*** 関数を提供します。ドライバ.

*直接 oid 要求インターフェイス*は、標準の oid 要求インターフェイスに似ています。 たとえば、 [**NdisFDirectOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest)関数と[*Filterdirectoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request)関数は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)関数と[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数に似ています。

**注**  NDIS 6.1 以降では、直接 oid 要求インターフェイスで使用する特定の oid がサポートされています。 NDIS 6.1 および一部の NDIS 6.1 Oid より前に存在していた Oid はサポートされていません。 直接 oid インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。 たとえば、「 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID を追加する」のメモを参照してください。

 

フィルタードライバーは、シリアル化されていない直接 OID 要求を処理できる必要があります。 標準の OID 要求インターフェイスとは異なり、NDIS では直接 OID 要求を直接 oid インターフェイスまたは標準の OID 要求インターフェイスと共に送信される他の要求と共にシリアル化しません。 また、フィルタードライバーは、IRQL &lt;= ディスパッチ\_レベルで直接 OID 要求を処理できる必要があります。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request" data-raw-source="[&lt;em&gt;FilterDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request)"><em>FilterDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request" data-raw-source="[&lt;em&gt;FilterOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)"><em>FilterOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_direct_oid_request" data-raw-source="[&lt;em&gt;FilterCancelDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_direct_oid_request)"><em>FilterCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request" data-raw-source="[&lt;em&gt;FilterCancelOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request)"><em>FilterCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request_complete" data-raw-source="[&lt;em&gt;FilterDirectOidRequestComplete&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request_complete)"><em>FilterDirectOidRequestComplete</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete" data-raw-source="[&lt;em&gt;FilterOidRequestComplete&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)"><em>FilterOidRequestComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest)"><strong>NdisFDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest" data-raw-source="[&lt;strong&gt;NdisFOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)"><strong>NdisFOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceldirectoidrequest" data-raw-source="[&lt;strong&gt;NdisFCancelDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceldirectoidrequest)"><strong>NdisFCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceloidrequest" data-raw-source="[&lt;strong&gt;NdisFCancelOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceloidrequest)"><strong>NdisFCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





