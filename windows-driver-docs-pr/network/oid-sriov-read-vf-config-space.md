---
title: OID_SRIOV_READ_VF_CONFIG_SPACE
description: ネットワークアダプターの指定された PCIe 仮想機能 (VF) に対して PCI Express (PCIe) の構成領域からデータを読み取るために、OID_SRIOV_READ_VF_CONFIG_SPACE のオブジェクト識別子 (OID) メソッドの要求が、それに関連するドライバーによって発行されます。
ms.assetid: 48CD54F5-F18F-4BC1-A93A-A824EC041605
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_READ_VF_CONFIG_SPACE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ab7850e6b3abf5a44b5c720376a4c5438297d00d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843981"
---
# <a name="oid_sriov_read_vf_config_space"></a>OID\_SRIOV\_読み取り\_VF\_CONFIG\_SPACE


それより前のドライバーは、オブジェクト識別子 (OID) のメソッド要求を OID\_SRIOV\_読み取り\_VF\_CONFIG の\_領域から、指定された PCIe 仮想機能 (VF) のデータを読み取ります。ネットワークアダプター。

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれます。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_SRIOV は、VF の PCI 構成領域の読み取り操作のためのパラメーターを格納する[ **\_vf\_CONFIG\_\_を読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)ます。

-   PCI 構成領域から読み取るデータ用の追加のバッファー領域。

<a name="remarks"></a>注釈
-------

VF ミニポートドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 このため、VF ミニポートドライバーは、VF の PCI 構成領域などのハードウェアリソースに直接アクセスすることはできません。 VF の PCI 構成領域にアクセスできるのは、PCIe 物理機能 (PF) のミニポートドライバーだけです。 PF ミニポートドライバーは、Hyper-v 親パーティションの管理オペレーティングシステムで実行され、VF リソースへの特権アクセスを持ちます。

VF PCI 構成領域を読み取るために、管理オペレーティングシステムで実行されているドライバーが oid\_oid の OID メソッド要求を発行し、\_VF\_CONFIG\_SPACE を PF ミニポートドライバーに読み取り\_ます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

たとえば、管理オペレーティングシステムで実行されている仮想化スタックは、VF ミニポートドライバーが[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)に対して\_SRIOV を呼び出したときに、\_VF\_CONFIG\_領域を読み取る oid メソッド\_要求を発行します。VF PCI 構成領域から読み取ります。

Oid\_oid の OID メソッド要求を処理するときに、\_VF\_CONFIG\_SPACE\_読み取るために、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf の[ **\_\_vf\_CONFIG\_\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造に含まれていた、以前のリソースがあることを確認する必要があります。済み. ミニポートドライバーは、Oid\_の oid メソッド要求を通じて VF のリソースを割り当てます。これにより[\_vf\_割り当て、NIC\_切り替わり](oid-nic-switch-allocate-vf.md)ます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   ミニポートドライバーは、要求された PCIe 構成領域のデータを返すために十分な大きさ**のバッファー (** [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造) を確認する必要があります。 これが true でない場合、ドライバーは OID 要求を失敗させる必要があります。
-   通常、ミニポートドライバーは[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)を呼び出して、要求された PCIe 構成領域に対してクエリを実行します。 ただし、ミニポートドライバーは、PCIe 構成領域の以前の読み取り操作または書き込み操作からドライバーがキャッシュした VF の PCIe 構成領域データも返すことができます。

    **注**  、独立系ハードウェアベンダー (IHV) が sr-iov[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の一部として仮想バスドライバー (VBD) を提供している場合、そのミニポートドライバーは[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)を呼び出すことができません。 代わりに、ドライバーは、プライベート通信チャネルを介して、VBD とのインターフェイスを使用して、.VBD に[*Readvfconfigblock*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))を呼び出すように要求する必要があります。 この関数は、基になる仮想 PCI (VPCI) バスドライバーでサポートされている[GUID\_vpci\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)インターフェイスから公開されています。

     

PF ミニポートドライバーが OID 要求を正常に完了できる場合、ドライバーは、要求された PCI 構成領域のデータを、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーによって参照されるバッファーにコピーする必要があります. ドライバーは、NDIS\_SRIOV の**Bufferoffset**メンバーによって指定されたオフセット位置にあるバッファーにデータをコピーし[ **\_\_VF\_CONFIG\_SPACE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体を読み取ります。

詳細については、「[仮想関数の PCI 構成データのクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-configuration-data-of-a-virtual-function)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_SRIOV の OID メソッド要求について、次のいずれかの状態コードを返します。これは、\_VF\_CONFIG\_SPACE\_読み取ります。

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
<td><p>ミニポートドライバーがシングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)"><strong>NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_の\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)

[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)

[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[*ReadVfConfigBlock*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))

 

 




