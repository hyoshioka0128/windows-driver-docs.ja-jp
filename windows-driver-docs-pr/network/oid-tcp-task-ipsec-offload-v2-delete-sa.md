---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA
description: セットとして、TCP/IP トランスポートは OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA OID を使用して、指定されたセキュリティアソシエーション (SAs) を NIC から削除するように要求します。
ms.assetid: 9b2c702c-beaa-4caf-97c5-d80a2632e4d3
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: aa796160d0667580eb9d4f4401fd5d7b6d524d8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843885"
---
# <a name="oid_tcp_task_ipsec_offload_v2_delete_sa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA の削除


\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]

設定として、TCP/IP トランスポートでは、IPSEC\_オフロード\_V2\_\_SA OID を削除する OID を使用して、\_\_\_TCP を使用して、指定されたセキュリティアソシエーション (SAs) を NIC から削除するように要求します。

**注**  NDIS では、この oid が直接 oid 要求インターフェイスでサポートされています。 直接 OID 要求インターフェイスの詳細については、「 [NDIS 6.1 DIRECT Oid Request interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

<a name="remarks"></a>注釈
-------

IPsec オフロードバージョン 2 (IPsecOV2) をサポートするすべての NDIS 6.1 ミニポートドライバーは、この OID をサポートする必要があります。

ミニポートドライバーがこの要求を受信すると、ドライバーは NIC から指定された SAs を削除し、SAs に割り当てられたすべてのシステムリソースを解放する必要があります。

ミニポートドライバーは、 [**IPSEC\_オフロード\_V2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)を受信します。 sa バンドルへのハンドルと、次の**IPSEC\_オフロード\_V2**へのポインターを含む sa 構造体を\_削除し\_sa を削除\_ます。リンクリスト内の構造体。

ミニポートドライバーでは、 [**NDIS\_IPSEC\_オフロード\_V2\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体を受信[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) **に設定でき**ます。データ. TCP/IP トランスポートは、その後、IPSEC\_オフロード\_V2 を\_IPSEC オフロード\_V2\_SA を削除してパケットを受信した受信 SA を一度削除してから、送信 SA を削除するためにもう一度 SA を\_\_します。これは、削除された受信 SA に対応します。 NIC は、対応する OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA 要求を削除する前に、これらの SAs のいずれかを削除することはできません。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、この要求に対して次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポートドライバーが要求を正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポートドライバーは、要求を非同期的に完了します。 ミニポートドライバーはすべての処理を完了した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>関数を呼び出し、 <em>STATUS</em>パラメーターに<strong>NDIS_STATUS_SUCCESS</strong>を渡すことによって、要求を成功させる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポートドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポートドライバーが要求の処理を停止しました。 たとえば、NDIS は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>Miniportresetex</em></a>関数を呼び出しました。</p></td>
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
<td><p>バージョン</p></td>
<td><p>NDIS 6.1 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_\_SA の削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)

[**NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

 

 




