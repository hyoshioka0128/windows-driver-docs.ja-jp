---
title: OID_SRIOV_SET_VF_POWER_STATE
description: ネットワークアダプターの指定された PCI Express (PCIe) 仮想関数 (VF) の電源状態を変更するために、OID_SRIOV_SET_VF_POWER_STATE のオブジェクト識別子 (OID) セット要求が発生します。
ms.assetid: 9723518E-2312-48F9-820A-19F5567A33DB
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_SET_VF_POWER_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 06e2c85565a0f5ae3feba00cec75982bab1a8102
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843977"
---
# <a name="oid_sriov_set_vf_power_state"></a>OID\_SRIOV\_設定\_VF\_電源\_状態


それより前のドライバーは、OID のオブジェクト識別子 (OID) セット要求を発行\_SRIOV\_\_VF\_電源\_状態を設定して、ネットワークアダプターの指定された PCI Express (PCIe) 仮想関数 (VF) の電源状態を変更します。 電源状態の変更は特権操作であるため、この OID セット要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 次に、PF ミニポートドライバーは、指定された電源状態を VF に設定します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_設定された、VF\_POWER\_STATE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

PF ミニポートドライバーがこの OID セット要求を発行するときは、次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf\_\_設定されていることを確認する必要があります[**vf\_POWER\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)構造には、以前のリソースが含まれています。済み. PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](oid-nic-switch-allocate-vf.md)れるため、vf のリソースを割り当てます。 指定した VF が割り当て済みの状態でない場合、ドライバーは OID 要求を失敗させる必要があります。

-   電源状態操作は、指定された VF にのみ影響する必要があります。 この操作は、同じネットワークアダプター上の他の VFs または PF に影響しないようにする必要があります。

詳細については、「[仮想関数の電源状態の設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-power-state-of-a-virtual-function)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_SRIOV の OID セット要求について、次のいずれかの状態コードを返します。これは、\_VF\_電力\_状態\_設定されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)"><strong>NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_設定\_VF\_電源\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

 

 




