---
title: OID_NIC_SWITCH_DELETE_SWITCH
description: NDIS は、ネットワーク アダプターから NIC スイッチを削除する OID_NIC_SWITCH_DELETE_SWITCH のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 5785B30F-B67F-4D5A-A93A-243D33B9CAE8
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_DELETE_SWITCH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9bb973eaf620f8fe23c1d21ab8ca0f7b26c2dda0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362896"
---
# <a name="oidnicswitchdeleteswitch"></a>OID\_NIC\_スイッチ\_削除\_スイッチ


OID のオブジェクト識別子 (OID) セット要求を発行する NDIS\_NIC\_切り替える\_削除\_スイッチ、ネットワーク アダプターから NIC スイッチを削除します。

NDIS は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) にこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**注**  などプロトコルまたはフィルター ドライバー、ドライバー、スライド PF ミニポート ドライバーにこの OID メソッド要求を発行できません。

 

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_削除\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)構造体。

<a name="remarks"></a>コメント
-------

OID の OID の要求を設定する\_NIC\_切り替える\_削除\_スイッチの OID メソッド要求を既に作成されている NIC スイッチを削除します[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)します。

OID の OID メソッド要求を受け取ったとき\_NIC\_スイッチ\_削除\_スイッチ、PF ミニポート ドライバーでは、次を実行する必要があります。

1.  PF のミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合は、指定した NIC スイッチに関連付けられているソフトウェア リソースを解放にする必要があります。 ただし、ドライバーのみを解放できますハードウェア リソースの NIC を切り替えるときに[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)が呼び出されます。

    静的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの作成を静的](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)します。

2.  PF ミニポート ドライバーでは、動的な作成と NIC のスイッチの構成をサポートする場合、指定した NIC スイッチに関連付けられているハードウェアおよびソフトウェア リソースを無料する必要があります。

    動的な NIC スイッチの作成の詳細については、次を参照してください。 [NIC スイッチの動的な作成](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)です。

3.  ドライバーが呼び出すことによってに、アダプターで仮想化を無効にする必要があります、PF ミニポート ドライバーでは、動的に作成し、NIC のスイッチが削除されているすべてをサポートする場合[ **NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)します。 ネットワーク アダプターの設定を仮想化を無効にする必要があります、 *EnableVirtualization*パラメーターを FALSE と*NumVFs*パラメーターを 0 にします。

    [**NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)クリア、 **NumVFs**メンバーと**VF 有効**の PCI 構成領域で SR-IOV 拡張機能の構造内のビット、ネットワーク アダプターの PF.

    **注**  PF ミニポート ドライバーでは、静的な作成と NIC のスイッチの構成をサポートする場合のみ呼び出す必要があります[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)とき[*MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)が呼び出されます。

     

詳細については、次を参照してください。 [NIC スイッチを削除する](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数は、次のいずれかがこの要求の値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
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
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)"> <em>MiniportResetEx</em> </a>関数。</p></td>
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
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)"> <strong>NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_NIC\_スイッチ\_削除\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_スイッチ\_FREE\_VF](oid-nic-switch-free-vf.md)

 

 




