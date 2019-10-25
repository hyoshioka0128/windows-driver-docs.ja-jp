---
title: OID_NIC_SWITCH_CREATE_VPORT
description: ネットワークアダプターの NIC スイッチに既定以外の仮想ポート (VPort) を作成するために、OID_NIC_SWITCH_CREATE_VPORT のオブジェクト識別子 (OID) メソッドの要求が、後のドライバーによって発行されます。
ms.assetid: 31109117-2242-40E0-B215-0FAE014B2035
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NIC_SWITCH_CREATE_VPORT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f525f3da17bb5316f06db571c1de70a9329818f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844098"
---
# <a name="oid_nic_switch_create_vport"></a>OID\_NIC\_スイッチ\_作成\_VPORT


ネットワークアダプターの NIC スイッチで既定以外の仮想ポート (VPort) を作成するために\_VPORT を作成\_ために、オブジェクト識別子 (OID) メソッドによる OID\_\_の要求が、そのドライバーによって発行されます。 この OID メソッド要求では、作成した VPort をネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) または以前に割り当てられた PCIe 仮想機能 (VF) に接続することもできます。

その後のドライバーは、この OID メソッド要求をネットワークアダプターの PF のミニポートドライバーに発行します。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)へのポインターが含まれています。 vport\_PARAMETERS 構造体\_ます。

<a name="remarks"></a>注釈
-------

このドライバーは、 [**NDIS\_NIC\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体を初期化して、作成する既定以外の vport に関する構成情報を指定します。 構成情報には、既定以外の VPort が接続されている PCIe 関数と、既定以外の VPort のキューペアの数が含まれます。

PF ミニポートドライバーが OID 要求を発行すると、ドライバーは、指定された既定以外の VPort に関連付けられているハードウェアとソフトウェアのリソースを割り当てます。 すべてのリソースが正常に割り当てられると、PF ミニポートドライバーは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)から NDIS\_STATUS\_SUCCESS を返すことによって OID を正常に完了します。

OID\_NIC\_スイッチ\_作成\_VPORT 要求が正常に完了した場合、PF ミニポートドライバーとそれ以降のドライバーは、後続の操作のために既定以外の VPort の**VPortId**値を保持する必要があります。 **VPortId**の値は、次の操作中に使用されます。

-   NDIS およびそれ以降のドライバーでは、 **VPortId**値を使用して、この vport に関連する oid 要求 ( [oid\_nic\_スイッチ\_VPORT\_パラメーター](oid-nic-switch-vport-parameters.md)および[oid\_NIC など) で、既定以外の vport を識別します。\_スイッチ\_\_VPORT を削除](oid-nic-switch-delete-vport.md)します。

-   送信操作中、NDIS は、パケットの送信元の VPort を識別する**VPortId**値を指定します。 この値は、帯域外 (OOB) [**NDIS\_net\_buffer\_\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)に指定されており、 [net\_buffer\_list](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)構造体の\_情報データをフィルター処理しています。

-   受信操作中、PF ミニポートドライバーは、パケットを転送する**VPortId**値を指定します。 この値は、OOB [**NDIS\_net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)でも指定されており、 [net\_buffer\_list](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)構造体の\_情報データをフィルター処理\_ます。

詳細については、「[仮想ポートの作成](https://docs.microsoft.com/windows-hardware/drivers/network/creating-a-virtual-port)」を参照してください。

既定の VPort は常に存在し、oid の OID 要求\_NIC の要求によって作成されてい**ない  、** \_VPORT を作成\_\_スイッチです。 既定の VPort には、NDIS\_既定\_VPORT\_ID の識別子が設定されています。 PF ミニポートドライバーが NIC スイッチを作成すると、ドライバーは自動的に既定の VPort をネットワークアダプターの PF に接続します。

 

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS または PF ミニポートドライバーは、oid\_NIC\_スイッチの OID メソッド要求について、次のいずれかの状態コードを返し\_スイッチ\_作成します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>) 未満です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS\_NIC\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[NET\_BUFFER\_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_スイッチ\_パラメーター](oid-nic-switch-parameters.md)

[OID\_NIC\_スイッチ\_VPORT\_パラメーター](oid-nic-switch-vport-parameters.md)

 

 




