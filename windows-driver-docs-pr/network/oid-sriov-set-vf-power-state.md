---
title: OID_SRIOV_SET_VF_POWER_STATE
description: 上にある、ドライバーは、電源状態の指定された PCI Express (PCIe) 仮想機能 (VF)、ネットワーク アダプターを変更する OID_SRIOV_SET_VF_POWER_STATE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 9723518E-2312-48F9-820A-19F5567A33DB
ms.date: 08/08/2017
keywords: -OID_SRIOV_SET_VF_POWER_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a6f8d73086a5f7ba2e10d92cd23e92a548c71fec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582278"
---
# <a name="oidsriovsetvfpowerstate"></a>OID\_SRIOV\_設定\_VF\_POWER\_状態


上にある、ドライバーの OID オブジェクト識別子 (OID) セット要求を発行する\_SRIOV\_設定\_VF\_POWER\_の状態が電源の状態の指定された PCI Express (PCIe) 仮想機能 (VF) を変更しますネットワーク アダプター。 電源状態の変更が特権操作のため、上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF) のミニポート ドライバーをこの OID セット要求を発行します。 PF のミニポート ドライバー、VF で指定された電源の状態を設定します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_設定\_VF\_POWER\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451683)構造体。

<a name="remarks"></a>コメント
-------

PF ミニポート ドライバーには、この OID セットの要求が発行される、次のガイドラインに従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_設定\_VF\_POWER\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451683)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 割り当てられた状態で指定された VF でない場合、ドライバーは OID 要求に失敗する必要があります。

-   電源状態の操作は、指定 VF のみに影響する必要があります。 操作では、その他の VFs または同じネットワーク アダプターの PF には影響する必要があります。

詳細については、[仮想関数の状態の電源設定](https://msdn.microsoft.com/library/windows/hardware/hh440230)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

OID OID の要求の設定の次のステータス コードのいずれかの PF ミニポート ドライバー返します\_SRIOV\_設定\_VF\_POWER\_状態。

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
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451683" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451683)"> <strong>NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_設定\_VF\_POWER\_状態\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451683)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




