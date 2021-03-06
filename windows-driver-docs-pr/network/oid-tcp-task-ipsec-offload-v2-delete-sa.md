---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA
description: TCP/IP トランスポートは、セットとして、ミニポート ドライバーが NIC から指定されたセキュリティ アソシエーション (Sa) を削除することを要求する OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA OID を使用してください。
ms.assetid: 9b2c702c-beaa-4caf-97c5-d80a2632e4d3
ms.date: 08/08/2017
keywords: -OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c8dac562bbb94f93e5c1e6be09cfa1f79af6ac6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353699"
---
# <a name="oidtcptaskipsecoffloadv2deletesa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA


\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートが、OID を使用して、セットとして\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA OID ミニポート ドライバーが、指定したセキュリティを削除することを要求するにはNIC からアソシエーション (Sa)

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、次を参照してください。 [NDIS 6.1 Direct OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

<a name="remarks"></a>注釈
-------

IPsec をサポートするすべての NDIS 6.1 ミニポート ドライバーでは、バージョン 2 (IPsecOV2) は、この OID をサポートする必要がありますをオフロードします。

ミニポート ドライバーでは、この要求を受信したときに、ドライバーは、NIC から指定された SAs を削除し、SAs の割り当てられたシステム リソースを解放する必要があります。

ミニポート ドライバーが、受信、 [ **IPSEC\_オフロード\_V2\_削除\_SA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_delete_sa) SA のバンドルを識別するハンドルとへのポインターを含む構造体次**IPSEC\_オフロード\_V2\_削除\_SA**リンク リストの構造体。

ミニポート ドライバーを設定できます**SaDeleteReq**で、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)受信構造[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 TCP/IP トランスポートは、OID を後で発行\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA を 1 回、着信 SA 経由で受信したパケットを削除するには削除された着信 SA に対応する送信の SA を削除するには、もう一度です。 NIC 削除しないでこれらの SAs のいずれかの対応する OID を受信する前に\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA 要求。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)"> <em>MiniportResetEx</em> </a>関数。</p></td>
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
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_削除\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)

[**NDIS\_IPSEC\_OFFLOAD\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

 

 




