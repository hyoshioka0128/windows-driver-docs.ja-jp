---
title: OID_SRIOV_RESET_VF
description: このドライバーは、OID_SRIOV_RESET_VF のオブジェクト識別子 (OID) セット要求を発行して、シングルルート i/o 仮想化をサポートするネットワークアダプターの指定された PCI Express (PCIe) 仮想関数 (VF) をリセットします。
ms.assetid: 7D5EB64B-3345-478A-8D42-192939C0B9C2
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_RESET_VF ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 37fdf0a0cf1f6f98941c9ccb5f3e26b53822f9ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843979"
---
# <a name="oid_sriov_reset_vf"></a>OID\_SRIOV\_リセット\_VF


このドライバーは、オブジェクト識別子 (OID) set 要求を OID\_SRIOV\_\_リセットして、単一ルート i/o 仮想化をサポートするネットワークアダプターで、指定された PCI Express (PCIe) 仮想関数 (VF) をリセットします。 この OID セット要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_RESET\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)構造体へのポインターが含まれています。 前のドライバーは、この構造体の**VFId**メンバーによってリセットされる VF の識別子を指定します。

<a name="remarks"></a>注釈
-------

VF は、PCI Express (PCIe) の関数レベルのリセット (FLR) を使用してリセットできます。 FLR 要求は特権操作であるため、Hyper-v 親パーティションの管理オペレーティングシステムで実行されている PF ミニポートドライバーによってのみ実行できます。 管理オペレーティングシステムで実行されるその後のドライバーは、FLR 要求の通知を受け、oid の OID セット要求を SRIOV\_リセット\_VF を PF ミニポートドライバーにリセット\_ます。

この OID 要求を処理するとき、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された VF [ **\_PARAMETERS 構造\_\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)され、以前に割り当てられたリソースがあることを確認する必要があります。 PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](oid-nic-switch-allocate-vf.md)れるため、vf のリソースを割り当てます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   リセット操作は、指定された VF にのみ影響する必要があります。 この操作は、同じネットワークアダプター上の他の VFs または PF に影響しないようにする必要があります。

詳細については、「[仮想関数のリセット](https://docs.microsoft.com/windows-hardware/drivers/network/resetting-a-virtual-function)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、OID の set 要求に対して次のいずれかの状態コードを返します\_SRIOV\_リセット\_VF です。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_RESET_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)"><strong>NDIS_SRIOV_RESET_VF_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
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

[**NDIS\_SRIOV\_リセット\_VF\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

 

 




