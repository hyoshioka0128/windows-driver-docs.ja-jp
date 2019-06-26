---
title: 省電力プロトコル オフロードの追加と削除
description: 省電力プロトコル オフロードの追加と削除
ms.assetid: f00f13b4-9204-4480-884a-407684a4b2d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ee07ef24464e7f9394f492e1e10b59eba11f46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383726"
---
# <a name="adding-and-deleting-low-power-protocol-offloads"></a>省電力プロトコル オフロードの追加と削除





NDIS プロトコル ドライバーがの OID セット要求を発行する低電力プロトコルの負荷を軽減させるには、 [OID\_PM\_追加\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体。

**注**  ネットワーク アダプターが、パケットに応答する必要があり、コンピューターをスリープ解除、着信パケットには、(たとえば、構成エラー) のためのオフロードのプロトコルとパターンの両方が一致すると、します。

 

[ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)構造体には、次の情報が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>優先順位</strong></p></td>
<td align="left"><p>プロトコルのオフロードの優先度が含まれています。 重なっている場合より高い優先度のプロトコルのプロトコルの詳細のオフロードの使用可能なリソースがない場合に負荷を軽減、リソースを解放する低優先度プロトコル オフロード削除 NDIS ドライバーを追加します。 ミニポート ドライバーでは、このメンバーを無視する必要があります。 プロトコル ドライバーは、NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_HIGHEST に NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_LOWEST から定義済みの範囲内の任意の値を指定できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadType</strong></p></td>
<td align="left"><p>含まれています、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)"> <strong>NDIS_PM_PROTOCOL_OFFLOAD_TYPE</strong> </a>プロトコルの種類を指定する値の負荷を軽減します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FriendlyName</strong></p></td>
<td align="left"><p>含まれています、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_counted_string" data-raw-source="[&lt;strong&gt;NDIS_PM_COUNTED_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_counted_string)"> <strong>NDIS_PM_COUNTED_STRING</strong> </a>低電力プロトコルのユーザーが判読できる説明を含む構造体の負荷を軽減します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadId</strong></p></td>
<td align="left"><p>オフロードされたプロトコルを識別する NDIS で提供される値が含まれています。 NDIS の OID 要求を送信する前に<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload" data-raw-source="[OID_PM_ADD_PROTOCOL_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)">OID_PM_ADD_PROTOCOL_OFFLOAD</a>を基になる NDIS ドライバーにダウンするか、上位のドライバーでは、NDIS セットへの要求が完了すると<strong>ProtocolOffloadId</strong>にある値プロトコル間で一意で、ネットワーク アダプターにオフロードします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NextProtocolOffloadOffset</strong></p></td>
<td align="left"><p>OID 要求の開始のオフセットを含む<em>InformationBuffer</em>、[次へ] を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)"> <strong>NDIS_PM_PROTOCOL_OFFLOAD</strong> </a>構造体のリストで、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list" data-raw-source="[OID_PM_PROTOCOL_OFFLOAD_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)">OID_PM_PROTOCOL_OFFLOAD_LIST</a> OID。 OID_PM_PROTOCOL_OFFLOAD_LIST の詳細については、次を参照してください。<a href="obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md" data-raw-source="[Obtaining the Current Parameter Settings of Low Power Protocol Offloads](obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md)">取得、現在のパラメーターの設定の低電力プロトコルの負荷を軽減</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadParameters</strong></p></td>
<td align="left"><p>いずれかが含まれています、 <strong>IPv4ARPParameters</strong>、 <strong>IPv6NSParameters</strong>、または<strong>Dot11RSNRekeyParameters</strong>共用体の構造体。</p>
<p></p>
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IPv4ARPParameters</p></td>
<td align="left"><p>IPv4 ARP パラメーターが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6NSParameters</p></td>
<td align="left"><p>IPv6 近隣要請 (NS) のパラメーターが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dot11RSNRekeyParameters</p></td>
<td align="left"><p>IEEE 802.11 堅牢なセキュリティで保護されたネットワーク (RSN) ハンドシェイクのパラメーターが含まれています</p></td>
</tr>
</tbody>
</table>
<p> </p></td>
</tr>
</tbody>
</table>

 

NDIS はすべてオフロード プロトコルにネットワーク アダプターの一意の識別子を割り当てます。 プロトコルのオフロード識別子では、各ネットワーク アダプターのオフロードがプロトコルの一意の値が。 ただし、プロトコル オフロード識別子はグローバルに一意なすべてのネットワーク アダプターです。 NDIS は、NDIS 送信するとき、基になるミニポート ドライバーにこの識別子を渡します、 [OID\_PM\_追加\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)ミニポート ドライバーに OID 要求。 プロトコルのオフロードが成功した場合は、NDIS はオフロード プロトコル上にあるドライバーに識別子を返します。 上にあるドライバーでは、識別子を使用して、以前にオフロードされたプロトコルを削除します。 プロトコルのオフロード識別子は、オフロードのプロトコルがネットワーク アダプターから削除されたときにも上層のドライバーに状態インジケーターに使用されます。

プロトコル ドライバーする必要がありますすべて削除オフロードされたプロトコルのネットワーク アダプターからそのネットワーク アダプターにバインドを閉じる前にします。 プロトコル ドライバーを低電力プロトコルのオフロードを削除するには、OID セット要求を送信します[OID\_PM\_削除\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-protocol-offload)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、プロトコルのオフロード識別子へのポインターが含まれています。

NDIS では、同じネットワーク アダプターにプロトコルのオフロードを追加する複数の NDIS プロトコル ドライバーを許可します。 オフロード プロトコルの数が要求されたときに、適切な一連のプロトコルがネットワーク アダプターにオフロードされことを確認するのにはネットワーク アダプターでサポートできるよりも高い、プロトコルのドライバーがオフロード プロトコルごとに優先順位を割り当てます。 NDIS は、ネットワーク アダプターがリソース不足になるために、新しい優先度の高いプロトコルをオフロードできない、NDIS は低優先度のオフロード プロトコルのいずれか (ある場合) を削除し、もう一度、優先度の高いプロトコルの負荷を軽減しようとしています。

**注**  ミニポート ドライバーが失敗する低電力プロトコル オフロード追加を要求し、状態を返す\_NDIS\_PM\_プロトコル\_オフロード\_一覧\_NDIS 再プロトコルの優先順位を許可するすべての状態コードの負荷を軽減します。

 

場合、プロトコルがオフロードいずれかの優先順位の低い優先度の高いプロトコル、オフロードの結果として、削除すると、NDIS 送信、 [ **NDIS\_状態\_PM\_オフロード\_REJECTED**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)上にある削除済みのプロトコルを設定するドライバーに通知の状態を示す値をオフロードします。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造には、拒否されたのプロトコルのオフロード識別子が含まれていますプロトコルのオフロードします。 NDIS のプロトコルのオフロード識別子を提供する、 **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体。

 

 





