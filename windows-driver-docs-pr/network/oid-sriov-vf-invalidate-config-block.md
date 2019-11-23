---
title: OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
description: NDIS は、1つまたは複数の構成ブロック内のデータが変更された PCI Express (PCIe) 仮想機能 (VF) のミニポートドライバーに通知するために、OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CF73E0DA-20DA-49A0-80B0-0F5A56DCEF5D
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
ms.localizationpriority: medium
ms.openlocfilehash: 54838ce21ac6c3a5a1007429ce026109b6d79c33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843975"
---
# <a name="oid_sriov_vf_invalidate_config_block"></a>OID\_SRIOV\_VF\_無効\_構成\_ブロック


NDIS は、オブジェクト識別子 (OID) メソッドの OID\_SRIOV\_VF\_\_\_無効にして、1つまたは複数の構成ブロック内のデータが変更された PCI Express (PCIe) 仮想関数 (VF) のミニポートドライバーに通知します。 NDIS は、PCIe 物理機能 (PF) のミニポートドライバーが[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)を呼び出すときに、この OID を発行します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)へのポインターが含まれており\_CONFIG\_BLOCK\_INFO 構造体\_無効にします。 この構造体は、PF ミニポートドライバーによってデータが変更 (*無効*) された1つまたは複数の仮想関数 (VF) 構成ブロックを指定します。

<a name="remarks"></a>注釈
-------

VF 構成ブロックは、PF および VF ミニポートドライバー間のバックチャネル通信に使用されます。 IHV は、デバイスに対して1つまたは複数の VF 構成ブロックを定義できます。 各 VF 構成ブロックには、IHV によって定義された形式、長さ、およびブロック ID があります。

  **注**各 VF 構成ブロックのデータは、PF および vf ミニポートドライバーによってのみ使用されます。

 

VF 構成データは、次のドライバー間で交換されます。

-   VF ドライバー。ゲストオペレーティングシステムで実行されます。 このオペレーティングシステムは、Hyper-v 子パーティション内で実行されます。

-   管理オペレーティングシステムで実行される PF ドライバー。 このオペレーティングシステムは、Hyper-v の親パーティション内で実行されます。

無効な VF 構成データの通知を処理するために、NDIS およびミニポートドライバーは次の手順を実行します。

1.  ゲストオペレーティングシステムでは、NDIS は[**IOCTL\_VPCI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)の i/o 制御要求を発行し、\_ブロック要求を無効に\_します。 この IOCTL が完了すると、NDIS には、VF 構成データが変更されたことが通知されます。

2.  管理オペレーティングシステムでは、次の手順が実行されます。

    1.  PF ミニポートドライバーは、 [**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)関数を呼び出して、VF 構成データが変更され、無効になったことを NDIS に通知します。 ドライバーは、どの VF 構成ブロックが変更されたかを指定する ULONGLONG ビットマスクに*Blockmask*パラメーターを設定します。 ビットマスクの各ビットは、VF 構成ブロックに対応します。 ビットが1に設定されている場合は、対応する VF 構成ブロック内のデータが変更されます。
    2.  NDIS は、管理オペレーティングシステムで実行される仮想化スタックを、VF 構成ブロックデータの変更について通知します。 仮想化スタックは、 *Blockmask*パラメーターデータをキャッシュします。

        **注**  PF ミニポートドライバーが[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)を呼び出すたびに、仮想化スタックは、*ブロックマスク*パラメーターデータにキャッシュ内の現在の値を指定します。

         

    3.  仮想化スタックは、ゲストオペレーティングシステムで実行されている仮想 PCI (VPCI) ドライバーに、VF 構成データの無効化について通知します。 仮想化スタックは、キャッシュされた*Blockmask*パラメーターデータを vpci ドライバーに送信します。

3.  ゲストオペレーティングシステムでは、次の手順が実行されます。

    1.  VPCI ドライバーは、キャッシュされた*blockmask*パラメーターデータを Vpci の**blockmask**メンバーに保存し、 [**IOCTL\_vpci**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)に関連付けられている[ **\_ブロック\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)構造体を無効にして、ブロック要求を無効に\_\_します。\_

    2.  VPCI ドライバーは[**IOCTL\_vpci\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)正常に完了し、ブロック要求を\_無効にします。 これが発生すると、NDIS は oid\_oid の OID メソッド要求を発行し\_VF\_無効\_構成\_、VF ミニポートドライバーにブロックします。 [**NDIS\_SRIOV\_VF\_無効\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)は OID 要求で渡されます。\_ この構造体には、キャッシュされた*Blockmask*パラメーターのデータが含まれます。

        また、NDIS では、別の[**IOCTL\_VPCI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)も発行されます。これにより、VF 構成データへの変更の継続的な通知を処理するために、ブロック要求\_ブロックが発生

    3.  VF ドライバーが OID\_処理するとき\_VF\_無効\_構成\_ブロック要求は、指定された VF 構成ブロックからデータを読み取ります。

シングルルート i/o 仮想化 (SR-IOV) インターフェイス内でのバックチャネル通信の詳細については、「sr-iov [PF/VF バックチャネル通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーは、oid\_SRIOV\_VF の OID メソッド要求について、次のいずれかの状態コードを返し\_CONFIG\_BLOCK を無効に\_ます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"><strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。SET_INFORMATION。BytesNeeded</strong>構造体のサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"></a>が必要です。</p></td>
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
[**IOCTL\_VPCI\_\_ブロックを無効にします**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_によって\_構成\_ブロック\_情報が無効になります**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)

[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_SPACE](oid-sriov-read-vf-config-space.md)

[**VPCI\_\_ブロック\_出力を無効にします**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)

 

 




