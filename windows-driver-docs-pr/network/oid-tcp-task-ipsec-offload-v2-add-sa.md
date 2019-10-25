---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA
description: セットとして、TCP/IP トランスポートは OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA OID を使用して、指定されたセキュリティアソシエーション (SAs) を NIC に追加するように要求します。
ms.assetid: bd1d0cf2-234d-4c06-904e-fe2de6022981
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: cbe156d3c4aeaaf86dd146852ad83529114fb8a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843887"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加\_


\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]

設定として、TCP/IP トランスポートでは、IPSEC\_オフロード\_V2 を\_するための OID\_TCP\_タスクを使用し\_SA OID を追加して、指定されたセキュリティアソシエーション (SAs) を NIC に追加するように要求します。

**注**  NDIS では、この oid が直接 oid 要求インターフェイスでサポートされています。 直接 OID 要求インターフェイスの詳細については、「 [NDIS 6.1 DIRECT Oid Request interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

**  この**OID は、NDIS 6.1 および6.20 でサポートされています。 NDIS 6.30 以降のドライバーについては、「 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)」を参照してください。

 

<a name="remarks"></a>注釈
-------

IPsec オフロードバージョン 2 (IPsecOV2) をサポートするすべての NDIS 6.1 および6.20 ミニポートドライバーは、この OID をサポートする必要があります。

TCP/IP トランスポートは、NIC が IPsecOV2 操作を実行できることを確認した後、SAs を追加するようにミニポートドライバーに要求します。 トランスポートが SA を追加する前に、トランスポートは IPsecOV2 操作を NIC にオフロードできません。

ミニポートドライバーは、 [**ipsec\_オフロード\_V2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)を受信し、次の IPSEC\_オフロード\_V2 へのポインターを含む\_SA 構造体を追加して、リンクリストに\_SA 構造体を追加します。 ミニポートドライバーは、SAs の IPsecOV2 処理用に NIC を構成します。 正常に OID に設定された\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加すると、ミニポートドライバーによって、IPSEC の**Offloadhandle**メンバー内のオフロード SAs を識別するハンドルが提供され\_オフロード\_V2\_\_SA を追加します。 (たとえば、トランスポートは、送信パスのハンドルを使用して、使用するオフロード SA を示します)。 リンクリスト内のいずれかの SAs がオフロードされた場合、設定要求は成功します。

ミニポートドライバーは OID 要求のエラー状態を返すことがあります。たとえば、NIC の容量が不足しているために、より多くの SAs をオフロードすることができます。 また、競合状態を回避する必要があるため、ミニポートドライバーがエラー状態を返すことがあります。 この場合、NIC の構成が変更され、特定のアルゴリズムが除外されます。

要求が失敗した場合、リンクリスト内の SAs はオフロードされていません。 リンクリスト内の特定の SA でエラーが発生した場合、ミニポートドライバーは、対応する IPSEC\_オフロード\_V2\_\_SA 構造体を**NULL**に追加するための**offloadhandle**メンバーを設定する必要があります。

ミニポートドライバーは、初期化時に、 [**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体の**Saoffloadcapacity**メンバーで NIC がサポートできる SAs の最大数を報告します。 必要に応じて、TCP/IP トランスポートによって、 [IPSEC\_オフロード\_V2\_\_sa oid\_\_\_](oid-tcp-task-ipsec-offload-v2-delete-sa.md)設定して、ミニポートドライバーが NIC から sa を削除するように要求することができます。

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
<td><p>NDIS 6.1 および6.20 でサポートされています。 NDIS 6.30 以降の場合は、 <a href="oid-tcp-task-ipsec-offload-v2-add-sa-ex.md" data-raw-source="[OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)">OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX</a>を使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_\_SA を追加する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)

[**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA の削除](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




