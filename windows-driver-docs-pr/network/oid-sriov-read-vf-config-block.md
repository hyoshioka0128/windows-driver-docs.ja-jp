---
title: OID_SRIOV_READ_VF_CONFIG_BLOCK
description: 上にある、ドライバーは、PCI Express (PCIe) 仮想機能 (VF) の指定された構成ブロックからデータを読み取る OID_SRIOV_READ_VF_CONFIG_BLOCK のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: A7AC7A18-5DA2-4EE8-B635-04616ABFE08C
ms.date: 08/08/2017
keywords: -OID_SRIOV_READ_VF_CONFIG_BLOCK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bdf18e367143a494207497d7ae88a48d6efef281
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362884"
---
# <a name="oidsriovreadvfconfigblock"></a>OID\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_SRIOV\_読み取り\_VF\_CONFIG\_ブロックから、指定された PCI Express (PCIe) 仮想機能 (VF) データの読み取り構成ブロック。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)のオフセットを含む構造体VF 構成ブロックから読み取られるデータを格納しているバッファー内の場所をこの構造体の先頭からのバイト単位の単位。

-   指定された VF 構成ブロックから読み取るデータの追加バッファー領域。

<a name="remarks"></a>コメント
-------

VF 構成ブロックは、PF と VF のミニポート ドライバーの間のバック チャネル通信に使用されます。 IHV は、ミニポート ドライバーの 1 つ以上の VF 構成ブロックを定義できます。 各 VF 構成ブロックは、IHV で定義された形式、長さ、およびブロック id。

**注**  各 VF 構成ブロックからのデータは、PF と VF のミニポート ドライバーでのみ使用します。

 

OID の OID メソッド要求を発行する前に\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック、重なって、ドライバーがのメンバーを設定する必要があります[ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)次のように構造体。

-   設定、 **VFId**メンバーを元の情報が読み取られる VF の識別子。

-   設定、 **BlockId**メンバーを元の情報が読み取られる VF 構成ブロックの識別子。

-   設定、**長さ**構成ブロックから読み取るバイト数のメンバー。

-   設定、 **BufferOffset** 、バッファー内のオフセットにメンバー (によって参照される**InformationBuffer**メンバー) 指定された VF 構成ブロックから読み取られるデータにが含まれます。 このオフセットがの先頭からバイト単位で指定された、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体。

OID の OID メソッド要求を処理するときに\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック、PF ミニポート ドライバーが次のガイドラインに従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   PF のミニポート ドライバーは、ことを確認する必要があります、 **BlockId**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体が有効な VF 構成ブロックを指定します。 それ以外の場合は、ドライバーは OID 要求に失敗する必要があります。

シングル ルート I/O 仮想化 (SR-IOV) インターフェイス内でのバック チャネル通信の詳細については、次を参照してください。 [SR-IOV PF/VF のバック チャネル通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)します。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID のメソッドの要求に関する次の状態コードのいずれかを返します\_SRIOV\_読み取り\_VF\_CONFIG\_をブロックします。

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
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)"> <strong>NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 ミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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

[**NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](oid-sriov-read-vf-config-space.md)

 

 




