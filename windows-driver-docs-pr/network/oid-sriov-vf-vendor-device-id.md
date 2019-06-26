---
title: OID_SRIOV_VF_VENDOR_DEVICE_ID
description: 上にある、ドライバーは、オブジェクト識別子 (OID) メソッドへの要求を OID_SRIOV_VF_VENDOR_DEVICE_ID の PCI Express (PCIe) デバイス識別子 (DeviceID) と、PCI Express (PCIe) 仮想機能 (VF) ネットワーク アダプターの仕入先 id (VendorID) クエリを発行します。 この仮想ネットワーク アダプターは、VF に関連付けられている HYPER-V 子パーティションで公開されます。上にあるドライバーは、、PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。
ms.assetid: 19D98264-325B-4EA4-83BF-BBFECD185E55
ms.date: 08/08/2017
keywords: -OID_SRIOV_VF_VENDOR_DEVICE_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6ce3875d1b5986a9d5a2c0c901cdb9c471010acb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373892"
---
# <a name="oidsriovvfvendordeviceid"></a>OID\_SRIOV\_VF\_ベンダー\_デバイス\_ID


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_SRIOV\_VF\_ベンダー\_デバイス\_PCI Express (PCIe) デバイス識別子 (DeviceID) と仕入先にクエリ IDPCI Express (PCIe) 仮想機能 (VF) ネットワーク アダプター (VendorID) の識別子です。 この仮想ネットワーク アダプターは、VF に関連付けられている HYPER-V 子パーティションで公開されます。

上にあるドライバーは、、PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造体。

<a name="remarks"></a>注釈
-------

この OID メソッド要求を発行して、前に、上にあるドライバーを初期化する必要があります、 [ **NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造体し、設定する必要があります、 **VFId**メンバーを元の情報が読み取られる VF の識別子。

この OID 要求を処理する場合、PF ミニポート ドライバーする必要があります指定 VF に以前割り当てられたリソースを確認します。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

詳細については、次を参照してください。[仮想関数、PCI ベンダーとデバイスのデバイス Id の照会](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function)します。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_SRIOV\_VF\_ベンダー\_デバイス\_id。

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
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)"> <strong>NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




