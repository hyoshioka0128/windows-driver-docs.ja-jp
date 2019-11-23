---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS は、ネットワークアダプターに NIC スイッチを作成するために OID_NIC_SWITCH_CREATE_SWITCH のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_CREATE_SWITCH
ms.localizationpriority: medium
ms.openlocfilehash: 185eb66205c98cef3e6df73e078db59395d8c8bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844099"
---
# <a name="oid_nic_switch_create_switch"></a>OID\_NIC\_スイッチ\_作成\_スイッチ


NDIS は、OID のオブジェクト識別子 (OID) メソッド要求を発行\_NIC\_スイッチ\_作成\_スイッチを作成して、ネットワークアダプターに NIC スイッチを作成します。 この OID 要求を処理するときに、ミニポートドライバーは、アダプターに NIC スイッチのリソースを割り当てます。

NDIS は、この OID メソッド要求を、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行します。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

**注**  プロトコルやフィルタードライバーなどのそれ以降のドライバーは、OID\_NIC\_スイッチの oid メソッド要求を発行できません。これは、PF ミニポートドライバーへのスイッチ\_作成\_ます。

 

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

OID\_\_スイッチの oid メソッド要求を受信すると\_スイッチ\_作成されますが、PF ミニポートドライバーは次の操作を行う必要があります。

1.  PF ミニポートドライバーが静的スイッチの作成と構成をサポートしている場合は、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出したときに NIC スイッチが作成されます。 ドライバーは、この OID 要求を処理するときに、 [**NDIS\_NIC\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体の構成パラメーターを確認する必要があります。 パラメーターは、 *MiniportInitializeEx*の呼び出し中にスイッチを作成するためにドライバーによって使用されるものと同じである必要があります。 これが true でない場合、ドライバーは OID 要求を失敗させる必要があります。

    詳細については、「 [NIC スイッチの静的作成](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)」を参照してください。

2.  PF ミニポートドライバーで動的スイッチの作成と構成がサポートされている場合、ドライバーは、NDIS\_NIC の構成値を検証し、 [ **\_PARAMETERS 構造\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)を設定して、これらの値に基づいて nic スイッチを作成する必要があります。

    詳細については、「 [NIC スイッチの動的作成](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)」を参照してください。

3.  PF ミニポートドライバーは、NIC スイッチの既定の VPort に必要なハードウェアおよびソフトウェアリソースを割り当てる必要があります。

    既定の VPort は常に oid 要求 oid\_NIC の要求を使用して作成され**ます  \_** スイッチ\_作成\_、oid\_の oid 要求を使用して\_スイッチ\_削除\_スイッチ[削除](oid-nic-switch-delete-switch.md)します。 Oid\_の OID 要求、 [nic\_スイッチ\_\_vport](oid-nic-switch-create-vport.md)と[oid\_nic\_\_の削除\_vport](oid-nic-switch-delete-vport.md)を使用して、nic スイッチで既定以外の vport を作成および削除します。

     

4.  ダイナミックスイッチの作成と構成をサポートする PF ミニポートドライバーでは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出すことによって、スイッチで sr-iov の仮想化を有効にする必要があります。 この呼び出しにより、アダプターの PCI Express (PCIe) 構成領域の SR-IOV 拡張機能構造で**Numvfs**メンバーと**VF Enable** bit が構成されます。

    SR-IOV 構成領域の詳細については、「PCI SIG の[シングルルート I/o 仮想化と共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)の仕様」を参照してください。

    **注**  PF ミニポートドライバーが静的スイッチの作成をサポートしている場合は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が呼び出されたときにスイッチを作成した後に sr-iov の仮想化が有効になります。

     

PF ミニポートドライバーが oid\_\_の oid の OID メソッド要求を正常に完了した場合は\_スイッチ\_作成して、次のようにすることができます。

-   Oid の OID メソッド要求を使用して、VFs を NIC スイッチに割り当てることができます。 [\_nic\_スイッチ\_](oid-nic-switch-allocate-vf.md)によって\_VF が割り当てられます。

-   Oid\_\_NIC の oid メソッド要求を使用して NIC スイッチに既定以外の VPorts を作成することができます。これには、 [\_vports\_作成](oid-nic-switch-create-vport.md)ます。

この OID 要求の処理方法の詳細については、「OID\_NIC の処理」を参照してください。 [\_スイッチ要求を作成\_には\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/handling-the-oid-nic-switch-create-switch-request)を使用してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid\_NIC\_スイッチの OID メソッド要求について、次のいずれかの状態コードを返し\_スイッチ\_作成します。

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
<td><p>PF ミニポートドライバーは sr-iov インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>) 未満です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_NIC\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

 

 




