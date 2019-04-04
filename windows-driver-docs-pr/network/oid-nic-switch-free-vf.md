---
title: OID_NIC_SWITCH_FREE_VF
description: 上にある、ドライバーは、ネットワーク アダプターの PCI Express (PCIe) 仮想機能 (VF) リソースを解放する OID_NIC_SWITCH_FREE_VF のオブジェクト識別子 (OID) セット要求を発行します。上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。
ms.assetid: B1A72D34-286A-4A70-8BE3-F21324B92187
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_FREE_VF ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5469c272ed6c52721e0c2a3e374b5a8811f341c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560350"
---
# <a name="oidnicswitchfreevf"></a>OID\_NIC\_スイッチ\_FREE\_VF


OID のオブジェクト識別子 (OID) セット要求を発行する上位のドライバー\_NIC\_スイッチ\_FREE\_VF のネットワーク アダプターの PCI Express (PCIe) 仮想機能 (VF) リソースを解放します。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451579)構造体。

上にあるドライバーを解放する VF の識別子を指定する、 **VFId**この構造体のメンバー。 ドライバーの以前の OID メソッド要求からこの識別子を取得した[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

<a name="remarks"></a>注釈
-------

OID の OID セット要求を発行する上位のドライバー\_NIC\_スイッチ\_FREE\_VF を VF のリソースを解放します。 これらのリソースがの OID メソッド要求を通じて割り当てられた以前[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

VF リソースを解放する方法の詳細については、[仮想関数のリソースを解放](https://msdn.microsoft.com/library/windows/hardware/hh439570)を参照してください。

**注**  そのドライバーは VF を同じリソースの解放が要求できる唯一のコンポーネントで上にある、ドライバーは VF のリソースの割り当てを要求するとします。 上にあるドライバーは、OID の OID セット要求を発行する必要があります\_NIC\_スイッチ\_FREE\_VF VF リソースを解放します。 ドライバーのによって割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)要求。

 

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>関数。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求の次のステータス コードのいずれかを返します。

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
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF のミニポート ドライバーが SR-IOV インターフェイスをサポートしないか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451579" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_FREE_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451579)"> <strong>NDIS_NIC_SWITCH_FREE_VF_PARAMETERS</strong> </a>構造が無効な値を指定します。 たとえば、 <strong>VFId</strong> VF のいずれかが割り当てられていないか削除されていない拡張を持つメンバーを指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451579)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_スイッチ\_削除\_スイッチ](oid-nic-switch-delete-switch.md)

 

 




