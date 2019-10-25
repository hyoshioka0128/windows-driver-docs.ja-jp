---
title: OID_NIC_SWITCH_DELETE_VPORT
description: 前のドライバーは、ネットワークアダプターの NIC スイッチで以前に作成された既定以外の仮想ポート (VPort) を削除するために、オブジェクト識別子 (OID) セット要求を OID_NIC_SWITCH_DELETE_VPORT に発行します。
ms.assetid: D762035C-33AC-4579-8EA0-6A422AE4CA76
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NIC_SWITCH_DELETE_VPORT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 12f18d5992499e64ce090d9e37bf3ae97ce0eed7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844091"
---
# <a name="oid_nic_switch_delete_vport"></a>OID\_NIC\_スイッチ\_削除\_VPORT


前のドライバーは、OID\_\_のオブジェクト識別子 (OID) セット要求を発行します。\_VPORT を削除して、ネットワークアダプターの NIC スイッチで以前に作成された既定以外の仮想ポート (VPort) を削除\_ます。 このドライバーでは、以前に作成した VPort を削除できます。これを行うには、oid\_NIC\_スイッチの OID メソッド要求を発行し[\_\_VPORT を作成](oid-nic-switch-create-vport.md)します。

この OID セット要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 この OID セット要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)へのポインターが含まれています\_VPORT\_PARAMETERS 構造体を削除\_ます。

<a name="remarks"></a>注釈
-------

プロトコルやフィルタードライバーなど、それより前のドライバーは、以前に作成した既定以外の仮想ポートのみを削除できます。 この後のドライバーでは、oid\_NIC\_スイッチの OID メソッド要求を発行して VPort を作成[\_\_VPORT を作成](oid-nic-switch-create-vport.md)します。

PF ミニポートドライバーが oid\_\_の oid 要求を受信すると、\_VPORT\_削除、ドライバーは、指定された VPort に割り当てられたハードウェアとソフトウェアのリソースを解放する必要があります。

詳細については、「[仮想ポートの削除](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-virtual-port)」を参照してください。

**注**  oid\_\_\_\_NIC の要求によって明示的に削除できるのは、既定以外の Vports だけです。 既定の VPort は、PF ミニポートドライバーによって既定の NIC スイッチが削除されると、暗黙的に削除されます。 詳細については、「 [NIC スイッチの削除](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)」を参照してください。

 

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_NIC\_スイッチの OID セット要求について、次のいずれかの状態コードを返し\_VPORT\_削除します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF ミニポートドライバーは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>) 未満です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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
[**NDIS\_NIC\_スイッチ\_\_VPORT\_パラメーターの削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_スイッチ\_削除\_スイッチ](oid-nic-switch-delete-switch.md)

 

 




