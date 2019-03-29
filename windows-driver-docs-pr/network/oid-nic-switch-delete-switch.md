---
title: OID_NIC_SWITCH_DELETE_SWITCH
description: NDIS は、ネットワーク アダプターから NIC スイッチを削除する OID_NIC_SWITCH_DELETE_SWITCH のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 5785B30F-B67F-4D5A-A93A-243D33B9CAE8
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_DELETE_SWITCH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 001a154a2c3de62ccbbdd19214011ed621bb0f66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573815"
---
# <a name="oidnicswitchdeleteswitch"></a>OID\_NIC\_スイッチ\_削除\_スイッチ


OID のオブジェクト識別子 (OID) セット要求を発行する NDIS\_NIC\_切り替える\_削除\_スイッチ、ネットワーク アダプターから NIC スイッチを削除します。

NDIS は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) にこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**注**  などプロトコルまたはフィルター ドライバー、ドライバー、スライド PF ミニポート ドライバーにこの OID メソッド要求を発行できません。

 

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_削除\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451575)構造体。

<a name="remarks"></a>コメント
-------

OID の OID の要求を設定する\_NIC\_切り替える\_削除\_スイッチの OID メソッド要求を既に作成されている NIC スイッチを削除します[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)します。

OID の OID メソッド要求を受け取ったとき\_NIC\_スイッチ\_削除\_スイッチ、PF ミニポート ドライバーでは、次を実行する必要があります。

1.  PF のミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合は、指定した NIC スイッチに関連付けられているソフトウェア リソースを解放にする必要があります。 ただし、ドライバーのみを解放できますハードウェア リソースの NIC を切り替えるときに[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が呼び出されます。

    静的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの作成を静的](https://msdn.microsoft.com/library/windows/hardware/hh440256)します。

2.  PF ミニポート ドライバーでは、動的な作成と NIC のスイッチの構成をサポートする場合、指定した NIC スイッチに関連付けられているハードウェアおよびソフトウェア リソースを無料する必要があります。

    動的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの動的な作成](https://msdn.microsoft.com/library/windows/hardware/hh406694)です。

3.  ドライバーが呼び出すことによってに、アダプターで仮想化を無効にする必要があります、PF ミニポート ドライバーでは、動的に作成し、NIC のスイッチが削除されているすべてをサポートする場合[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)します。 ネットワーク アダプターの設定を仮想化を無効にする必要があります、 *EnableVirtualization*パラメーターを FALSE と*NumVFs*パラメーターを 0 にします。

    [**NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)クリア、 **NumVFs**メンバーと**VF 有効**の PCI 構成領域で SR-IOV 拡張機能の構造内のビット、ネットワーク アダプターの PF.

    **注**  PF ミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合のみ呼び出す必要があります[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)とき[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が呼び出されます。

     

詳細については、次を参照してください。 [NIC スイッチを削除する](https://msdn.microsoft.com/library/windows/hardware/hh439415)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>関数。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求の次のステータス コードのいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF のミニポート ドライバーが SR-IOV インターフェイスをサポートしないか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451575" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451575)"> <strong>NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_NIC\_スイッチ\_削除\_スイッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451575)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_スイッチ\_FREE\_VF](oid-nic-switch-free-vf.md)

 

 




