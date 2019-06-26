---
title: OID_SRIOV_WRITE_VF_CONFIG_SPACE
description: 上にある、ドライバーは、データを書き込む PCI Express (PCIe) の構成領域を指定した PCIe 仮想機能 (VF) ネットワーク アダプターの OID_SRIOV_WRITE_VF_CONFIG_SPACE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 0D9866A6-A8C6-4B0A-8D17-A632E1AE37BF
ms.date: 08/08/2017
keywords: -OID_SRIOV_WRITE_VF_CONFIG_SPACE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0607a4c4dee27724070377c28e17d0a296df9496
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372502"
---
# <a name="oidsriovwritevfconfigspace"></a>OID\_SRIOV\_書き込み\_VF\_CONFIG\_領域


上位のドライバーの OID オブジェクト識別子 (OID) セット要求を発行する\_SRIOV\_書き込み\_VF\_CONFIG\_指定 PCIe の PCI Express (PCIe) の構成領域にデータを書き込む領域仮想機能 (VF) ネットワーク アダプターにします。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)を含む構造体、VF の PCI 構成領域の書き込み操作のパラメーターです。

-   PCI の構成領域に書き込まれるデータを含む追加のバッファー領域。

<a name="remarks"></a>注釈
-------

VF のミニポート ドライバーは、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 このため、VF のミニポート ドライバーは VF の PCI 構成領域などのハードウェア リソースを直接アクセスすることはできません。 PF ミニポート ドライバーのみ、HYPER-V 親パーティションの管理オペレーティング システムで実行されを VF の PCI 構成領域にアクセスできます。

など、仮想化スタックの上にある、ドライバーは、OID の OID のセット要求を発行\_SRIOV\_書き込み\_VF\_CONFIG\_VF のミニポート ドライバーを呼び出すときに領域[ **NdisMSetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata) PCI 構成領域に書き込めません。

OID の OID メソッド要求を処理するときに\_SRIOV\_書き込み\_VF\_CONFIG\_領域、PF ミニポート ドライバーには、次のガイドラインが従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーの OID メソッドの要求からの VF 用のリソースの割り当て[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

    指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   PF のミニポート ドライバー呼び出し[ **NdisMSetVirtualFunctionBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)要求 PCI 構成領域に書き込めません。 ただし、VF ドライバーが前のキャッシュの PCI 構成領域のデータの読み取りや書き込み PCI 構成領域の操作、PF ミニポート ドライバーも返します。

    **注**  独立系ハードウェア ベンダー (IHV) が SR-IOV 対応の一部としてバーチャル バス ドライバー (VBD) を提供する場合[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)、PF ミニポート ドライバーを呼び出してはならない[ **NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)します。 代わりに、ドライバーをプライベートな通信チャネルを介して VBD とのインターフェイスし、VBD を呼び出すことを要求する必要があります[ *SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_virtual_device_data)します。 この関数がから公開されている、 [GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)基になる仮想 PCI (VPCI) バス ドライバーによってサポートされているインターフェイス。

     

PF のミニポート ドライバーでは、OID 要求を正常に完了する場合、ドライバーは要求された PCI 構成の領域データをによって参照されるバッファーにコピーする必要があります、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 ドライバーで指定されたオフセットからバッファーにデータをコピーする**BufferOffset**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体。

詳細については、次を参照してください。[仮想関数の PCI 構成データを設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-pci-configuration-data-of-a-virtual-function)します。

### <a name="return-status-codes"></a>リターン状態コード

OID OID の要求の設定の次のステータス コードのいずれかの PF ミニポート ドライバー返します\_SRIOV\_書き込み\_VF\_CONFIG\_領域。

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
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)"> <strong>NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata)

[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](oid-sriov-read-vf-config-space.md)

[*SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_virtual_device_data)

 

 




