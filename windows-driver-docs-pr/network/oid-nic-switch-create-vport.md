---
title: OID_NIC_SWITCH_CREATE_VPORT
description: 上にある、ドライバーは、ネットワーク アダプターの NIC のスイッチの既定以外の仮想ポート (VPort) を作成する OID_NIC_SWITCH_CREATE_VPORT のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 31109117-2242-40E0-B215-0FAE014B2035
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_CREATE_VPORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 742bee63784913086d9e777607e401369c4c5ff1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383596"
---
# <a name="oidnicswitchcreatevport"></a>OID\_NIC\_スイッチ\_作成\_VPORT


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_NIC\_切り替える\_作成\_VPORT ネットワーク アダプターの NIC のスイッチの既定以外の仮想ポート (VPort) を作成します。 この OID メソッド要求には、ネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) または、以前に割り当てられた PCIe 仮想機能 (VF) を作成した VPort もアタッチします。

上にあるドライバーは、ネットワーク アダプターの PF. のミニポート ドライバーにこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

<a name="remarks"></a>注釈
-------

上にあるドライバーを初期化します、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構成情報を含む構造体既定を作成する VPort 以外。 構成情報には、先 VPort がアタッチされている既定以外と数、キュー ペア VPort 既定以外の PCIe 関数が含まれています。

PF のミニポート ドライバーには、OID 要求が発行される、ドライバーは指定した既定以外の VPort に関連付けられているハードウェアおよびソフトウェア リソースを割り当てます。 すべてのリソースが正常に割り当てられた後、PF ミニポート ドライバー、OID が正常に完了 NDIS を返すことによって\_状態\_から成功[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416).

場合、OID\_NIC\_スイッチ\_作成\_VPORT 要求が正常に完了すると、PF ミニポート ドライバーおよび上位のドライバーを保持する必要があります、 **VPortId**既定以外の値連続した操作の VPort します。 **VPortId**値は、これらの操作中に使用されます。

-   NDIS および上にあるドライバーを使用して、 **VPortId**を既定以外の連続する OID で VPort を識別する値を要求などに関連するこの VPort、 [OID\_NIC\_スイッチ\_VPORT\_パラメーター](oid-nic-switch-vport-parameters.md)と[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)します。

-   送信操作では中、NDIS を指定します、 **VPortId** VPort のパケットの送信元を識別する値。 バンドの外 (OOB) 内でこの値が指定されて[ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566567)のデータ、[NET\_バッファー\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff568412)構造体。

-   中に受信操作、PF ミニポート ドライバーを指定します、 **VPortId**パケットが転送される値。 この値は、OOB 内も指定[ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566567)データ、の[NET\_バッファー\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff568412)構造体。

詳細については、次を参照してください。[仮想ポートを作成する](https://msdn.microsoft.com/library/windows/hardware/hh439412)します。

**注**  VPort は常に存在し、ない既定値は OID の OID 要求を作成した\_NIC\_スイッチ\_作成\_VPORT します。 既定 VPort NDIS の識別子を持つ\_既定\_VPORT\_id。 PF のミニポート ドライバーでは、NIC のスイッチを作成するとき、ドライバーは自動的に既定 VPort をネットワーク アダプターの PF アタッチします。

 

### <a name="return-status-codes"></a>リターン状態コード

NDIS または PF ミニポート ドライバーの OID の OID メソッド要求は、次のステータス コードのいずれかを返します\_NIC\_スイッチ\_作成\_スイッチ。

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
<td><p>PF のミニポート ドライバーが SR-IOV インターフェイスをサポートしないか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451597" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451597)"> <strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451597" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451597)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451597)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[NET\_バッファー\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff568412)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

[OID\_NIC\_スイッチ\_VPORT\_パラメーター](oid-nic-switch-vport-parameters.md)

 

 




