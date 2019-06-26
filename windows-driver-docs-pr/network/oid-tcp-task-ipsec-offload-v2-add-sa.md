---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA
description: TCP/IP トランスポートは、セットとして、ミニポート ドライバーが NIC に指定されたセキュリティ アソシエーション (Sa) を追加することを要求する OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA OID を使用してください。
ms.assetid: bd1d0cf2-234d-4c06-904e-fe2de6022981
ms.date: 08/08/2017
keywords: -OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 84b3c1ad587d308c51a09c2e7bd5840b2cb0d444
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353714"
---
# <a name="oidtcptaskipsecoffloadv2addsa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA


\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートが、OID を使用して、セットとして\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA OID ミニポート ドライバーが、指定したセキュリティを追加することを要求するにはNIC にアソシエーション (Sa)

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、次を参照してください。 [NDIS 6.1 Direct OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

**注**  NDIS 6.1 と 6.20 が動作でこの OID がサポートされています。 NDIS 6.30 以降のドライバーを参照してください。 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)します。

 

<a name="remarks"></a>コメント
-------

すべての NDIS 6.1 と IPsec をサポートする 6.20 ミニポート ドライバーは、バージョン 2 (IPsecOV2) は、この OID をサポートする必要がありますをオフロードします。

TCP/IP トランスポートは、NIC が IPsecOV2 操作を実行できることを判断、TCP/IP トランスポートは、SAs を追加するミニポート ドライバーを要求します。 トランスポートは、トランスポートは、SA を追加する前に、NIC に IPsecOV2 操作をオフロードことはできません。

ミニポート ドライバーが、受信、 [ **IPSEC\_オフロード\_V2\_追加\_SA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_add_sa)次 IPSECへのポインターを含む構造体\_オフロード\_V2\_追加\_リンク リストで SA 構造体。 ミニポート ドライバーでは、SAs の処理 IPsecOV2 の NIC を構成します。 OID に正常に設定されている\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA、ミニポート ドライバーにオフロードされた SAs を識別するハンドルを提供します**OffloadHandle** IPSEC のメンバー\_オフロード\_V2\_追加\_SA です。 (たとえば、トランスポート ハンドルを使用して、送信パスで SA を使用してをオフロードすることを示します)。 オフロードされた SAs リンク リスト内のいずれかは、セットの要求が成功した場合。

ミニポート ドライバーを返せる OID 要求は、エラー状態など、NIC の複数の SAs をオフロードする容量が不足している場合。 また、ミニポート ドライバーは、競合状態を回避する必要があるために、エラー状態を返す可能性があります。 この場合は、NIC の構成が変更され、特定のアルゴリズムは含まれません。

要求が失敗した場合、リンクの一覧で、SAs のオフロードされました。 ミニポート ドライバーを設定する必要があります、リンク リストの特定の SA の障害が発生した場合、 **OffloadHandle**メンバーに対応する IPSEC\_オフロード\_V2\_追加\_SA構造体を**NULL**します。

SAs でサポートできる NIC の最大数を報告するミニポート ドライバー、 **SaOffloadCapacity**のメンバー、 [ **NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)初期化中に構造体。 かどうか、必要に応じて TCP/IP トランスポート設定できる、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)を要求する OIDミニポート ドライバー、SA を NIC から削除します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.1 と 6.20 が動作ではサポートされています。 NDIS 6.30 以降を使用して<a href="oid-tcp-task-ipsec-offload-v2-add-sa-ex.md" data-raw-source="[OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)">OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX</a>します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_追加\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_add_sa)

[**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




