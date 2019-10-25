---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX
description: セットとして、TCP/IP トランスポートは OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX OID を使用して、指定されたセキュリティアソシエーション (SAs) を NIC に追加するように要求します。
ms.assetid: 9D356CFA-3353-4E62-9B1C-0FF650DCE75C
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f0038311fbeb7573920fc4f31e5fc44b8265db9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843890"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa_ex"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_EX


\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]

設定として、TCP/IP トランスポートでは、IPSEC\_オフロード\_V2\_\_SA\_EX OID を追加して、指定されたセキュリティアソシエーション (SAs) を追加するように要求するために、\_TCP\_\_タスクを使用します。NIC に対して。

**注**  NDIS では、この oid が直接 oid 要求インターフェイスでサポートされています。 直接 OID 要求インターフェイスの詳細については、「 [NDIS 6.1 DIRECT Oid Request interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

<a name="remarks"></a>注釈
-------

IPsec オフロードバージョン 2 (IPsecOV2) をサポートするすべての NDIS 6.30 ミニポートドライバーは、この OID をサポートする必要があります。

TCP/IP トランスポートは、NIC が IPsecOV2 操作を実行できることを確認した後、SAs を追加するようにミニポートドライバーに要求します。 トランスポートが SA を追加する前に、トランスポートは IPsecOV2 操作を NIC にオフロードできません。

ミニポートドライバーは、SAs の IPsecOV2 処理用に NIC を構成します。 正常に OID に設定された\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA\_追加します。ミニポートドライバーは **、オフロード**SA を識別するハンドルを提供します。[**IPSEC\_オフロード\_V2\_\_SA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)構造体を追加します。 (たとえば、トランスポートは、送信パスのハンドルを使用して、使用するオフロード SA を示します)。 SA がオフロードされた場合、設定要求は成功します。

ミニポートドライバーは OID 要求のエラー状態を返すことがあります。たとえば、NIC の容量が不足しているために、より多くの SAs をオフロードすることができます。 また、競合状態を回避する必要があるため、ミニポートドライバーがエラー状態を返すことがあります。 この場合、NIC の構成が変更され、特定のアルゴリズムが除外されます。

要求が失敗した場合、SAs はオフロードされませんでした。 SA でエラーが発生した場合、ミニポートドライバーは、対応する IPSEC\_オフロード\_V2 の**Offloadhandle**メンバーを設定し\_\_SA\_EX 構造体を**NULL**に追加します。

ミニポートドライバーは、初期化時に、 [**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体の**Saoffloadcapacity**メンバーで NIC がサポートできる SAs の最大数を報告します。 必要に応じて、TCP/IP トランスポートによって、 [IPSEC\_オフロード\_V2\_\_sa oid\_\_\_](oid-tcp-task-ipsec-offload-v2-delete-sa.md)設定して、ミニポートドライバーが NIC から sa を削除するように要求することができます。

この OID は、基本的に以前のバージョン、 [oid\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA を追加](oid-tcp-task-ipsec-offload-v2-add-sa.md)するのと同じです。 唯一の違いは、更新された[**IPSEC\_OFFLOAD\_V2\_\_SA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)構造体を追加することです。

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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_\_SA\_EX を追加する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)

[**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加\_](oid-tcp-task-ipsec-offload-v2-add-sa.md)

[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA の削除](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




