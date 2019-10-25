---
title: プロトコル ドライバー Direct OID 要求
description: プロトコル ドライバー Direct OID 要求
ms.assetid: 387d27de-3214-4f93-8f45-9a2f28e5036f
keywords:
- 直接 OID 要求インターフェイス WDK ネットワーク
- 直接 OID 要求パス WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f815522b94ad090c89a7b226417f14633f905817
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844913"
---
# <a name="protocol-driver-direct-oid-requests"></a>プロトコル ドライバー Direct OID 要求





直接 OID 要求パスをサポートするために、プロトコルドライバーは、Ndis\_プロトコルの*Protocolxxx*関数のエントリポイントを提供します[ **\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics)の構造と**ndis は、** プロトコルドライバー。

*直接 oid 要求インターフェイス*は、標準の oid 要求インターフェイスに似ています。 たとえば、 [**NdisDirectOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest)関数と[**Protocoltoidrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete)関数は、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数と[**ProtocolOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)関数に似ています。

**注**  NDIS 6.1 以降では、直接 oid 要求インターフェイスで使用する特定の oid がサポートされています。 NDIS 6.1 および一部の NDIS 6.1 Oid より前に存在していた Oid はサポートされていません。 直接 oid インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。 たとえば、「 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID を追加する」のメモを参照してください。

 

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete)"><strong>ProtocolDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)"><strong>ProtocolOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest" data-raw-source="[&lt;strong&gt;NdisDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest)"><strong>NdisDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest" data-raw-source="[&lt;strong&gt;NdisOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)"><strong>NdisOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceldirectoidrequest" data-raw-source="[&lt;strong&gt;NdisCancelDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceldirectoidrequest)"><strong>NdisCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest" data-raw-source="[&lt;strong&gt;NdisCancelOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest)"><strong>NdisCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





