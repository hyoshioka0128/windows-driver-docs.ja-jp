---
title: OID_NIC_SWITCH_ALLOCATE_VF
description: 前のドライバーは、PCI Express (PCIe) 仮想関数 (VF) にリソースを割り当てるために、OID_NIC_SWITCH_ALLOCATE_VF のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CB88CE0C-705F-406B-90FE-FB206D6F4864
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_ALLOCATE_VF
ms.localizationpriority: medium
ms.openlocfilehash: 8da9ace40d3bfb1b7458475446dc645e6ca20af2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844104"
---
# <a name="oid_nic_switch_allocate_vf"></a>OID\_NIC\_スイッチ\_割り当て\_VF


その後のドライバーは、OID のオブジェクト識別子 (OID) メソッド要求を発行します。\_NIC\_スイッチ\_\_VF を割り当てて、PCI Express (PCIe) 仮想関数 (VF) のリソースを割り当てることができます。 VF は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートするネットワークアダプターで公開されます。

この OID メソッドの要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)へのポインターが含まれています。これは、VF\_PARAMETERS 構造体\_ます。

<a name="remarks"></a>注釈
-------

PF ミニポートドライバーは、ドライバーが OID のオブジェクト識別子 (OID) メソッドの要求を処理するときに、vf のソフトウェアリソースを割り当てます。\_NIC\_スイッチによって\_VF が割り当て\_ます。 ハードウェアリソースが VF に割り当てられている場合でも、PF ミニポートドライバーは、\_VF を割り当てる\_\_スイッチの OID\_正常に完了するまで、nonoperational と見なされます。

VF リソースの割り当て方法の詳細については、「[仮想関数のリソースの割り当て](https://docs.microsoft.com/windows-hardware/drivers/network/allocating-resources-for-a-virtual-function)」を参照してください。

1つのドライバーが VF のリソース割り当てを要求した後に、そのドライバーが同じ VF のリソースの解放を要求できる唯一のコンポーネントで**あることを  し**ます。 この後のドライバーは、oid\_NIC の OID セット要求を発行する必要があります。これは、 [\_空き\_vf の\_スイッチ](oid-nic-switch-free-vf.md)によって、vf リソースが解放されます。 前のドライバーを停止する前に、ドライバーの OID\_NIC\_スイッチによって割り当てられた各 VF のリソースを解放して\_VF 要求の割り当て\_する必要があります。

 

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_NIC\_スイッチの OID メソッド要求について、次のいずれかの状態コードを返し\_VF\_割り当てます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>) 未満です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[**NDIS\_\_RID を作成する**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[**NDIS\_NIC\_スイッチ\_VF\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[OID\_NIC\_スイッチ\_空き\_VF](oid-nic-switch-free-vf.md)

 

 




