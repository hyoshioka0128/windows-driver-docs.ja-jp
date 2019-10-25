---
title: OID_SRIOV_VF_VENDOR_DEVICE_ID
description: Pci express (pcie) 仮想機能 (VF) ネットワークアダプターの PCI Express (PCIe) デバイス識別子 (DeviceID) とベンダー識別子 (VendorID) にクエリを実行するために、OID_SRIOV_VF_VENDOR_DEVICE_ID のオブジェクト識別子 (OID) メソッドの要求を実行するドライバーが発生します。 この仮想ネットワークアダプターは、VF に接続されている Hyper-v 子パーティションで公開されます。この OID メソッドの要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。
ms.assetid: 19D98264-325B-4EA4-83BF-BBFECD185E55
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_VF_VENDOR_DEVICE_ID ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 731513521e7e5a9d41c0addd9560bdfc5fa7bcef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843972"
---
# <a name="oid_sriov_vf_vendor_device_id"></a>OID\_SRIOV\_VF\_ベンダ\_デバイス\_ID


VendorID の pci Express (PCIe) デバイス識別子 (DeviceID) とベンダー識別子 () に PCI Express のクエリを実行するために、そのドライバーは OID\_SRIOV\_VF\_\_\_ベンダのオブジェクト識別子 (OID) メソッド要求を発行します。PCIe仮想機能 (VF) ネットワークアダプター。 この仮想ネットワークアダプターは、VF に接続されている Hyper-v 子パーティションで公開されます。

この OID メソッドの要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_VF\_ベンダ\_デバイス\_ID\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

この OID メソッド要求を発行する前に、それ以降のドライバーは、 [**NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造を初期化する必要があります。また、 **VFID**メンバーを vf の識別子に設定する必要があります。情報の読み取り元の。

この OID 要求を処理するとき、PF ミニポートドライバーは、指定された VF に以前に割り当てられたリソースがあることを確認する必要があります。 PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](oid-nic-switch-allocate-vf.md)れるため、vf のリソースを割り当てます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

詳細については、「[仮想関数の PCI ベンダーおよびデバイス識別子のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_SRIOV\_VF\_ベンダー\_デバイス\_ID の OID メソッド要求について、次のいずれかの状態コードを返します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)"><strong>NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_SRIOV\_VF\_ベンダ\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

 

 




