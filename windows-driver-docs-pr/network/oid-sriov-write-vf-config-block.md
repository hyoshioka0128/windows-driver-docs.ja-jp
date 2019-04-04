---
title: OID_SRIOV_WRITE_VF_CONFIG_BLOCK
description: 上にある、ドライバーは、PCI Express (PCIe) 仮想機能 (VF) の構成ブロックにデータを書き込む OID_SRIOV_WRITE_VF_CONFIG_BLOCK のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 60527938-5627-482D-B94D-522DA8E32540
ms.date: 08/08/2017
keywords: -OID_SRIOV_WRITE_VF_CONFIG_BLOCK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 753364458f9d5a93ea4863d48a7a4bbb9f35631d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582167"
---
# <a name="oidsriovwritevfconfigblock"></a>OID\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック


上位のドライバーの OID オブジェクト識別子 (OID) セット要求を発行する\_SRIOV\_書き込み\_VF\_CONFIG\_PCI Express (PCIe) 仮想機能 (VF) の構成ブロックにデータを書き込むブロックします。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451687)のオフセットを含む構造体VF 構成ブロックに書き込まれたデータを格納しているバッファー内の場所をこの構造体の先頭からのバイト単位の単位。

-   指定された VF 構成ブロックに書き込まれるデータの追加バッファー領域。

<a name="remarks"></a>コメント
-------

VF 構成ブロックは、PF と VF のミニポート ドライバーの間のバック チャネル通信に使用されます。 IHV は、ミニポート ドライバーの 1 つ以上の VF 構成ブロックを定義できます。 各 VF 構成ブロックは、IHV で定義された形式、長さ、およびブロック id。

**注**  各 VF 構成ブロックからのデータは、PF と VF のミニポート ドライバーでのみ使用します。

 

OID の OID のセット要求を発行する前に\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック、重なって、ドライバーがのメンバーを設定する必要があります[ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451687)次のように構造体。

-   設定、 **VFId**メンバー情報が書き込まれるの VF の識別子。

-   設定、 **BlockId**メンバー情報が書き込まれる元の構成ブロックの識別子。

-   設定、**長さ**VF 構成ブロックに書き込むバイト数のメンバー。

-   設定、 **BufferOffset** 、バッファー内のオフセットにメンバー (によって参照される**InformationBuffer**メンバー) が指定された VF 構成ブロックから書き込まれるデータが含まれます。 このオフセットがの先頭からバイト単位で指定された、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451687)構造体。

OID の OID のセット要求を処理するときに\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック、PF ミニポート ドライバーが次のガイドラインに従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451687)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   PF のミニポート ドライバーは、ことを確認する必要があります、 **BlockId**のメンバー、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451687)構造体が有効な VF 構成ブロックを指定します。 それ以外の場合は、ドライバーは OID 要求に失敗する必要があります。

シングル ルート I/O 仮想化 (SR-IOV) インターフェイス内でのバック チャネル通信の詳細については、[SR-IOV PF/VF のバック チャネル通信](https://msdn.microsoft.com/library/windows/hardware/hh440251)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

OID OID の要求の設定の次のステータス コードのいずれかのミニポート ドライバー返します\_SRIOV\_書き込み\_VF\_CONFIG\_ブロックします。

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
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451687" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_BLOCK_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451687)"> <strong>NDIS_SRIOV_WRITE_VF_CONFIG_BLOCK_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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

[**NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451687)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](oid-sriov-read-vf-config-space.md)

 

 




