---
title: OID_NIC_SWITCH_ALLOCATE_VF
description: 上にある、ドライバーは、リソースを割り当てるため、PCI Express (PCIe) 仮想機能 (VF) OID_NIC_SWITCH_ALLOCATE_VF のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CB88CE0C-705F-406B-90FE-FB206D6F4864
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ALLOCATE_VF ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 866376c59289fadc45366ede9eb26fff78fdbfbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356132"
---
# <a name="oidnicswitchallocatevf"></a>OID\_NIC\_スイッチ\_ALLOCATE\_VF


上にある、ドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_NIC\_スイッチ\_割り当て\_VF の PCI Express (PCIe) 仮想機能 (VF) リソースを割り当てます。 VF は、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするネットワーク アダプターで公開されます。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。

<a name="remarks"></a>注釈
-------

PF のミニポート ドライバーでは、ドライバーの OID オブジェクト識別子 (OID) メソッド要求を処理する際に VF のソフトウェア リソースを割り当てます\_NIC\_スイッチ\_ALLOCATE\_VF します。 PF ミニポート ドライバーでは、OID が正常に完了するまでに操作不可状態にすると見なされる場合でも、ハードウェア リソースを VF に対して割り当てられている、\_NIC\_スイッチ\_ALLOCATE\_VF します。

VF リソースを割り当てる方法の詳細については、次を参照してください。[仮想関数のリソースを割り当てる](https://docs.microsoft.com/windows-hardware/drivers/network/allocating-resources-for-a-virtual-function)します。

**注**  上にある、ドライバーは VF のリソースの割り当てを要求、そのドライバーが同じ VF のリソースの解放が要求できる唯一のコンポーネント。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](oid-nic-switch-free-vf.md) VF リソースを解放します。 ドライバーの OID で割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に\_NIC\_スイッチ\_ALLOCATE\_VF 要求。

 

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_NIC\_スイッチ\_ALLOCATE\_VF します。

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
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_ように\_RID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[**NDIS\_NIC\_スイッチ\_VF\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[OID\_NIC\_スイッチ\_FREE\_VF](oid-nic-switch-free-vf.md)

 

 




