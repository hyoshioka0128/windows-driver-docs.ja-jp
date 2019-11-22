---
title: OID_SRIOV_WRITE_VF_CONFIG_SPACE
description: ネットワークアダプターの指定された PCIe 仮想機能 (VF) について、PCI Express (PCIe) 構成領域にデータを書き込むための OID_SRIOV_WRITE_VF_CONFIG_SPACE のオブジェクト識別子 (OID) セット要求が、その後のドライバーによって発行されます。
ms.assetid: 0D9866A6-A8C6-4B0A-8D17-A632E1AE37BF
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SRIOV_WRITE_VF_CONFIG_SPACE
ms.localizationpriority: medium
ms.openlocfilehash: 5745d1c52d5763e7cdacefec65101fba0f99ec8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843967"
---
# <a name="oid_sriov_write_vf_config_space"></a>OID\_SRIOV\_書き込み\_VF\_CONFIG\_SPACE


それより前のドライバーは、オブジェクト識別子 (OID) セットの OID\_の要求を発行します。この場合は、\_の\_\_VF の構成領域にデータを書き込むために、\_を設定します。ネットワークアダプター。

この OID セット要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_SRIOV\_、vf の PCI 構成領域の書き込み操作のためのパラメーターを格納する[ **\_vf\_CONFIG\_SPACE\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)構造体を書き込むことができます。

-   PCI 構成領域に書き込むデータを格納する追加のバッファー領域。

<a name="remarks"></a>注釈
-------

VF ミニポートドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 このため、VF ミニポートドライバーは、VF の PCI 構成領域などのハードウェアリソースに直接アクセスすることはできません。 Hyper-v の親パーティションの管理オペレーティングシステムで実行される PF ミニポートドライバーのみが、VF の PCI 構成領域にアクセスできます。

仮想化スタックなどの前のドライバーは、\_SRIOV\_の oid セット要求を発行します。これは、VF ミニポートドライバーが[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)を呼び出して PCI 構成領域に書き込むときに、\_VF\_CONFIG\_領域に書き込むことができます。

Oid\_oid の OID メソッド要求を処理するときに、\_VF\_CONFIG\_SPACE\_書き込む場合、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf の[ **\_\_vf\_CONFIG\_\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)構造に書き込まれ、以前のリソースがあることを確認する必要があります。済み. PF ミニポートドライバーは、Oid\_\_の oid メソッド要求を通じて VF のリソースを割り当て[\_vf\_割り当て](oid-nic-switch-allocate-vf.md)ます。

    指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   PF ミニポートドライバーは、 [**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)を呼び出して、要求された PCI 構成領域に書き込みます。 ただし、PF ミニポートドライバーは、PCI 構成領域の前の読み取り操作または書き込み操作からドライバーがキャッシュした VF の PCI 構成領域データも返すことができます。

    **注**  独立系ハードウェアベンダー (IHV) が sr-iov[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の一部として仮想バスドライバー (VBD) を提供している場合、その PF ミニポートドライバーは[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)を呼び出すことができません。 代わりに、ドライバーは、プライベート通信チャネルを介して、VBD とのインターフェイスを使用して、VBD が[*Setvirtualfunctiondata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)を呼び出すように要求する必要があります。 この関数は、基になる仮想 PCI (VPCI) バスドライバーでサポートされている[GUID\_vpci\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)インターフェイスから公開されています。

     

PF ミニポートドライバーが OID 要求を正常に完了できる場合、ドライバーは、要求された PCI 構成領域のデータを、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーによって参照されるバッファーにコピーする必要があります. ドライバーは、NDIS\_SRIOV の**Bufferoffset**メンバーによって指定されたオフセット位置にあるバッファーにデータをコピーし[ **\_\_VF\_CONFIG\_SPACE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体を読み取ります。

詳細については、「[仮想関数の PCI 構成データを設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-pci-configuration-data-of-a-virtual-function)する」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_SRIOV の OID セット要求について、次のいずれかの状態コードを返します。これは\_VF\_CONFIG\_SPACE\_書き込むことができます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)"><strong>NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。SET_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[GUID\_VPCI\_インターフェイス\_STANDARD](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_\_VF\_CONFIG\_の\_のパラメーターを書き込む**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)

[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_SPACE](oid-sriov-read-vf-config-space.md)

[*SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)

 

 




