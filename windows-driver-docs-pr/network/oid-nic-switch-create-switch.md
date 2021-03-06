---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS は、ネットワーク アダプターで NIC スイッチを作成する OID_NIC_SWITCH_CREATE_SWITCH のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_CREATE_SWITCH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 16518e741f3d35214a1e4ba0a13c68c0f1f3f1da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356133"
---
# <a name="oidnicswitchcreateswitch"></a>OID\_NIC\_スイッチ\_作成\_スイッチ


NDIS OID のオブジェクト識別子 (OID) メソッド要求の発行\_NIC\_切り替える\_作成\_NIC を作成するスイッチがネットワーク アダプターに切り替えます。 この OID 要求を処理する場合、ミニポート ドライバーは、アダプターで NIC スイッチのリソースを割り当てます。

NDIS は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) にこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**注**  OID の OID メソッドの要求を発行できないなど、プロトコルまたはフィルター ドライバー、ドライバー、スライド\_NIC\_スイッチ\_作成\_PF ミニポート ドライバーに切り替えます。

 

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体。

<a name="remarks"></a>コメント
-------

OID の OID メソッド要求を受け取ったとき\_NIC\_スイッチ\_作成\_スイッチ、PF ミニポート ドライバーでは、次を実行する必要があります。

1.  NDIS を呼び出すときは、NIC スイッチを作成しますが、PF ミニポート ドライバーでは、静的スイッチの作成と構成をサポートする場合[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。 構成パラメーターを確認する必要があります、ドライバーは、この OID 要求を処理する場合、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体。 パラメーターが呼び出し中に、スイッチを作成する、ドライバーによって使用されるものと同じにする必要があります*MiniportInitializeEx*します。 True でない場合、ドライバーは、OID 要求を失敗する必要があります。

    詳細については、次を参照してください。 [NIC スイッチの作成を静的](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)します。

2.  ドライバーの構成値を検証する必要があります、PF ミニポート ドライバーでは、動的なスイッチの作成と構成をサポートする場合、 [ **NDIS\_NIC\_切り替える\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体し、これらの値に基づいて、NIC のスイッチを作成します。

    詳細については、次を参照してください。 [NIC スイッチの動的な作成](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)です。

3.  PF ミニポート ドライバーでは、NIC のスイッチの既定 VPort のために必要なハードウェアおよびソフトウェア リソースを割り当てる必要があります。

    **注**  VPort が OID の OID 要求を使って作成された常に既定\_NIC\_スイッチ\_作成\_スイッチを介して、OID 要求の削除と[OID\_NIC\_スイッチ\_削除\_スイッチ](oid-nic-switch-delete-switch.md)します。 OID 要求[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)と[OID\_NIC\_スイッチ\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)作成と NIC のスイッチの拡張を既定以外の削除に使用されます。

     

4.  呼び出して、スイッチの SR-IOV 仮想化を有効にする必要があります動的スイッチの作成と構成をサポートしている PF ミニポート ドライバー [ **NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)します。 この呼び出しを構成、 **NumVFs**メンバーと**VF 有効**アダプターの構成領域の PCI Express (PCIe) の SR-IOV 拡張機能の構造内のビットします。

    SR-IOV 構成領域の詳細については、PCI SIG を参照してください。[シングル ルート I/O 仮想化および共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)仕様。

    **注**  スイッチを作成した後は、SR-IOV 仮想化を有効に、PF ミニポート ドライバーでは、静的スイッチの作成をサポートする場合と[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)が呼び出されます.

     

PF のミニポート ドライバーが OID の OID メソッド要求が正常に完了かどうか\_NIC\_スイッチ\_作成\_スイッチでは、次のようできます。

-   VFs を割り当てることができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

-   既定以外の拡張を作成することができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_作成\_VPORT](oid-nic-switch-create-vport.md)します。

この OID 要求を処理する方法の詳細については、次を参照してください。[処理 OID\_NIC\_スイッチ\_作成\_切り替え要求を](https://docs.microsoft.com/windows-hardware/drivers/network/handling-the-oid-nic-switch-create-switch-request)します。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_NIC\_スイッチ\_作成\_スイッチ。

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
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

 

 




