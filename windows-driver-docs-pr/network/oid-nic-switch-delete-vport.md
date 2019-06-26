---
title: OID_NIC_SWITCH_DELETE_VPORT
description: 上にある、ドライバーでは、ネットワーク アダプターの NIC のスイッチで既に作成済みの仮想ポート (VPort)、既定以外を削除する OID_NIC_SWITCH_DELETE_VPORT のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: D762035C-33AC-4579-8EA0-6A422AE4CA76
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_DELETE_VPORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 50293b1c30c2fc003251b77998b45466dd73e611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380845"
---
# <a name="oidnicswitchdeletevport"></a>OID\_NIC\_スイッチ\_削除\_VPORT


上位のドライバーの OID オブジェクト識別子 (OID) セット要求を発行する\_NIC\_スイッチ\_削除\_VPORT ネットワーク アダプターの NIC で作成した既定以外仮想ポート (VPort) を削除するにはスイッチです。 上にあるドライバーを削除の OID メソッド要求を発行してのみが以前作成した VPort [OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)します。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)構造体。

<a name="remarks"></a>注釈
-------

など、プロトコルまたはフィルター ドライバーの上にあるドライバーでは、既定以外が以前に作成した VPort のみ削除できます。 上にあるドライバーの OID メソッド要求を発行して、VPort を作成します[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)します。

PF のミニポート ドライバーが OID の OID 要求を受信すると\_NIC\_スイッチ\_削除\_VPORT、ドライバーは、指定した VPort に割り当てられたハードウェアとソフトウェア リソースを解放する必要があります。

詳細については、次を参照してください。[仮想ポートを削除する](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-virtual-port)します。

**注**  OID の OID 要求を通じて、拡張を明示的に削除できる以外のみ\_NIC\_スイッチ\_削除\_VPORT します。 PF のミニポート ドライバーが既定の NIC スイッチを削除するときに既定 VPort は暗黙的に削除されます。 詳細については、次を参照してください。 [NIC スイッチを削除する](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)します。

 

### <a name="return-status-codes"></a>リターン状態コード

OID OID の要求の設定の次のステータス コードのいずれかの PF ミニポート ドライバー返します\_NIC\_スイッチ\_削除\_VPORT します。

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
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"> <strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_スイッチ\_削除\_スイッチ](oid-nic-switch-delete-switch.md)

 

 




