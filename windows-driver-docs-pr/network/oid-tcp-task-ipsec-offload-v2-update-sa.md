---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
description: セットとして、TCP/IP トランスポートは OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA OID を使用して、ミニポートドライバーが NIC 上の指定されたセキュリティアソシエーション (SAs) を更新するように要求します。
ms.assetid: 22849103-9148-4621-b78f-b9f34f2c7ac1
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
ms.localizationpriority: medium
ms.openlocfilehash: a11b334360a2028f0d6342b2097e96750f0fbad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843883"
---
# <a name="oid_tcp_task_ipsec_offload_v2_update_sa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_更新\_SA


\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]

設定として、TCP/IP トランスポートは、IPSEC\_オフロード\_V2\_更新\_SA OID を\_する OID\_\_の OID を使用して、ミニポートドライバーが NIC 上の指定されたセキュリティアソシエーション (SAs) を更新するように要求します。

**注**  NDIS では、この oid が直接 oid 要求インターフェイスでサポートされています。 直接 OID 要求インターフェイスの詳細については、「 [NDIS 6.1 DIRECT Oid Request interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

<a name="remarks"></a>注釈
-------

IPsec オフロードバージョン 2 (IPsecOV2) をサポートするすべての NDIS 6.1 ミニポートドライバーは、この OID をサポートする必要があります。

ミニポートドライバーがこの要求を受信すると、ドライバーは NIC の指定された SAs を更新する必要があります。 SA が見つからない場合、または ESN がサポートされていない場合、ミニポートドライバーはこの要求を失敗させることができます。 この場合、返される状態は、"NDIS\_STATUS\_INVALID\_PARAMETER" になります。

ミニポートドライバーは、 [**ipsec\_オフロード\_V2\_更新プログラム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)に関する情報と、リンクリスト内の次の IPSEC\_オフロード\_V2\_更新\_sa 構造へのポインターを含む更新\_SA 構造体を受け取ります。

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


[**IPSEC\_OFFLOAD\_V2\_更新\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)

 

 




