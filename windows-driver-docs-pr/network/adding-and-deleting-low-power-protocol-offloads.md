---
title: 省電力プロトコル オフロードの追加と削除
description: 省電力プロトコル オフロードの追加と削除
ms.assetid: f00f13b4-9204-4480-884a-407684a4b2d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ea638ceb0b73dc26b5650ffd35925c50859104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838245"
---
# <a name="adding-and-deleting-low-power-protocol-offloads"></a>省電力プロトコル オフロードの追加と削除





低電力プロトコルオフロードを追加するために、NDIS プロトコルドライバーは oid\_PM の oid セット要求を発行し[\_\_プロトコル\_オフロードを追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造へのポインターが含まれています。

受信パケットがオフロードプロトコルとパターン (たとえば、構成エラーのため) と一致する場合、ネットワークアダプターはパケットに応答してコンピューターをウェイクアップする必要があります **。  **

 

[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)構造には、次の情報が含まれています。

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
<td align="left"><p><strong>的</strong></p></td>
<td align="left"><p>プロトコルオフロードの優先順位を格納します。 プロトコルのオフロードに使用できるリソースがないときに、追加のドライバーで優先度の高いプロトコルオフロードが追加された場合、NDIS はリソースを解放するために低優先度のプロトコルオフロードを削除することがあります。 ミニポートドライバーは、このメンバーを無視する必要があります。 プロトコルドライバーは、NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_LOWEST から NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_HIGHEST までの定義済みの範囲内の任意の値を提供できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadType</strong></p></td>
<td align="left"><p>プロトコルオフロードの種類を指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)"><strong>NDIS_PM_PROTOCOL_OFFLOAD_TYPE</strong></a>値を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>フレンドリ</strong></p></td>
<td align="left"><p>低電力プロトコルオフロードのユーザーが判読できる説明を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string" data-raw-source="[&lt;strong&gt;NDIS_PM_COUNTED_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string)"><strong>NDIS_PM_COUNTED_STRING</strong></a>構造体が含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadId</strong></p></td>
<td align="left"><p>オフロードプロトコルを識別する、NDIS によって提供される値が含まれます。 Ndis では、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload" data-raw-source="[OID_PM_ADD_PROTOCOL_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)">OID_PM_ADD_PROTOCOL_OFFLOAD</a>の OID 要求を基になる ndis ドライバーに送信する前、またはそれ以降のドライバーへの要求を完了する前に、 <strong>ProtocolOffloadId</strong>によって、プロトコルのオフロードで一意の値に設定されます。ネットワークアダプター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NextProtocolOffloadOffset</strong></p></td>
<td align="left"><p>OID 要求<em>Informationbuffer</em>の先頭であるオフセットを、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list" data-raw-source="[OID_PM_PROTOCOL_OFFLOAD_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)">OID_PM_PROTOCOL_OFFLOAD_LIST</a> oid のリスト内の次の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)"><strong>NDIS_PM_PROTOCOL_OFFLOAD</strong></a>構造体に格納します。 OID_PM_PROTOCOL_OFFLOAD_LIST の詳細については、「<a href="obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md" data-raw-source="[Obtaining the Current Parameter Settings of Low Power Protocol Offloads](obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md)">低電力プロトコルオフロードの現在のパラメーター設定を取得する</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadParameters</strong></p></td>
<td align="left"><p>共用体の<strong>IPv4ARPParameters</strong>、 <strong>IPv6NSParameters</strong>、または<strong>Dot11RSNRekeyParameters</strong>構造体のいずれかが含まれています。</p>
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
<td align="left"><p>IPv4 ARP パラメーターを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6NSParameters</p></td>
<td align="left"><p>IPv6 近隣要請 (NS) のパラメーターが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dot11RSNRekeyParameters</p></td>
<td align="left"><p>IEEE 802.11 の堅牢なセキュリティで保護されたネットワーク (RSN) ハンドシェイクパラメーターを含みます。</p></td>
</tr>
</tbody>
</table>
<p> </p></td>
</tr>
</tbody>
</table>

 

NDIS は、ネットワークアダプターに固有の識別子をすべてのオフロードプロトコルに割り当てます。 プロトコルオフロード識別子は、ネットワークアダプターでオフロードされるプロトコルごとに一意の値です。 ただし、プロトコルオフロード識別子は、すべてのネットワークアダプターでグローバルに一意ではありません。 Ndis は、NDIS が\_PM を送信するときに、この識別子を基になるミニポートドライバーに渡し、 [\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)oid 要求\_ミニポートドライバーに追加します。 プロトコルのオフロードが成功した場合、NDIS はプロトコルのオフロードを行う前のドライバーに識別子を返します。 前のドライバーは識別子を使用して、以前にオフロードされたプロトコルを削除します。 プロトコルオフロード識別子は、オフロードプロトコルがネットワークアダプターから削除されたときに、上位層ドライバーへの状態を示すためにも使用されます。

プロトコルドライバーは、ネットワークアダプターへのバインドを終了する前に、ネットワークアダプターからオフロードされたすべてのプロトコルを削除する必要があります。 低電力プロトコルオフロードを削除するために、プロトコルドライバーは oid\_PM の oid セット要求を送信し[\_\_プロトコル\_オフロードを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-protocol-offload)します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、プロトコルオフロード識別子へのポインターが含まれています。

NDIS では、複数の NDIS プロトコルドライバーで、同じネットワークアダプターにプロトコルオフロードを追加できます。 要求されたオフロードプロトコルの数がネットワークアダプターでサポートできる量より多い場合に、適切なプロトコルセットがネットワークアダプターにオフロードされるようにするため、プロトコルドライバーは各オフロードプロトコルに優先順位を割り当てます。 ネットワークアダプターにリソースが不足しているために、NDIS が新しい優先度のプロトコルをオフロードできない場合、NDIS は優先順位の低いオフロードプロトコル (存在する場合) のいずれかを削除し、優先度の高いプロトコルのオフロードを再試行します。

ミニポートドライバーは、低電力プロトコルのオフロードの追加要求を失敗させ、ndis\_PM\_プロトコル\_\_完全な状態コード\_一覧を\_返して、NDIS によっ**て  ** プロトコルのオフロード。

 

優先順位の低いプロトコルのオフロードの結果として、低優先度のオフロードプロトコルのいずれかが削除された場合、NDIS は、 [**ndis\_status\_PM\_オフロード\_拒否**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)状態の通知を送信します。削除されたプロトコルオフロードを設定します。 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、拒否されたプロトコルオフロードのプロトコルオフロード識別子が含まれています。 NDIS は、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体の**ProtocolOffloadId**メンバーにプロトコルオフロード識別子を提供しました。

 

 





