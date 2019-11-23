---
title: OID_NIC_SWITCH_DELETE_SWITCH
description: NDIS は、ネットワークアダプターから NIC スイッチを削除するために OID_NIC_SWITCH_DELETE_SWITCH のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 5785B30F-B67F-4D5A-A93A-243D33B9CAE8
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_DELETE_SWITCH
ms.localizationpriority: medium
ms.openlocfilehash: 7199d00167497b89a4f4a92d06f72d872289aaaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844094"
---
# <a name="oid_nic_switch_delete_switch"></a>OID\_NIC\_スイッチ\_削除\_スイッチ


NDIS は、OID のオブジェクト識別子 (OID) セット要求を発行\_NIC\_スイッチ\_削除\_スイッチを削除してネットワークアダプターから NIC スイッチを削除します。

NDIS は、この OID セット要求をネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行します。 この OID セット要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

**注**  プロトコルやフィルタードライバーなどのドライバーは、この OID メソッド要求を PF ミニポートドライバーに発行できません。

 

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、ndis\_NIC へのポインターが含まれています\_[ **\_スイッチ\_削除\_スイッチパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)構造体。

<a name="remarks"></a>注釈
-------

Oid\_NIC\_SWITCH\_DELETE\_スイッチの OID セット要求では、以前に作成された NIC スイッチが、Oid\_[NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)によって削除されます。

OID\_\_スイッチの oid メソッド要求を受信すると\_スイッチ\_削除されますが、PF ミニポートドライバーは次の操作を行う必要があります。

1.  PF ミニポートドライバーが NIC スイッチの静的な作成と構成をサポートしている場合は、指定された NIC スイッチに関連付けられているソフトウェアリソースを解放する必要があります。 ただし、ドライバーは、[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が呼び出されたときにのみ、NIC スイッチのハードウェアリソースを解放できます。

    静的 NIC スイッチの作成の詳細については、「 [Nic スイッチの静的作成](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)」を参照してください。

2.  PF ミニポートドライバーが NIC スイッチの動的作成と構成をサポートしている場合は、指定された NIC スイッチに関連付けられているハードウェアおよびソフトウェアリソースを解放する必要があります。

    動的な NIC スイッチの作成の詳細については、「 [Nic スイッチの動的作成](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)」を参照してください。

3.  PF ミニポートドライバーが動的作成をサポートしていて、すべての NIC スイッチが削除されている場合、ドライバーは[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出すことによって、アダプターの仮想化を無効にする必要があります。 仮想化を無効にするには、ネットワークアダプターで*Enablevirtualization*パラメーターを FALSE に設定し、 *numvfs*パラメーターを0に設定する必要があります。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)は、ネットワークアダプターの PF の PCI 構成領域にある Sr-iov 拡張機能構造の**numvfs**メンバーと**VF 有効化**ビットをクリアします。

    **注**  PF ミニポートドライバーが NIC スイッチの静的な作成と構成をサポートしている場合は、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が呼び出されたときにのみ[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出す必要があります。

     

詳細については、「 [NIC スイッチの削除](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)」を参照してください。

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

 

NDIS は、この要求に対して次のいずれかの状態コードを返します。

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
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF ミニポートドライバーは sr-iov インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS はデータを設定<strong>します。SET_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_NIC\_スイッチ\_削除\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_スイッチ\_空き\_VF](oid-nic-switch-free-vf.md)

 

 




