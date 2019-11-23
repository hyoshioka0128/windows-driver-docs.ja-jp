---
title: OID_NIC_SWITCH_VPORT_PARAMETERS
description: 1つ前のドライバーは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで作成された、NIC スイッチ上の仮想ポート (VPort) のパラメーターを取得できます。
ms.assetid: B22C760E-F2B0-4774-A532-4044C679CD64
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_VPORT_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: ab219b5898adbd4b4be3b0f7fd695873897bc7ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844075"
---
# <a name="oid_nic_switch_vport_parameters"></a>OID\_NIC\_スイッチ\_VPORT\_パラメーター


1つ前のドライバーは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで作成された、NIC スイッチ上の仮想ポート (VPort) のパラメーターを取得できます。 このドライバーは、これらのパラメーターを取得するために、オブジェクト識別子 (OID) のメソッド要求 OID\_NIC\_スイッチ\_VPORT\_パラメーターを発行します。

このようなドライバーは、OID\_NIC\_\_\_スイッチの OID セット要求を発行して、ネットワークアダプターの NIC スイッチに接続されている指定された VPort の構成パラメーターを設定します。 これらの OID セット要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。 これらの OID セット要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)へのポインターが含まれています。 vport\_PARAMETERS 構造体\_ます。

このドライバーは、 [**NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)の**VPortId**メンバーを vport\_PARAMETERS 構造\_vport に関連付けられている識別子に設定することにより、OID メソッドまたは Set 要求の vport を指定します。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

-   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](oid-nic-switch-create-vport.md)ます。

-   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](oid-nic-switch-enum-vports.md)ます。

<a name="remarks"></a>注釈
-------

Oid\_NIC\_スイッチ\_VPORT\_パラメーターは、 [oid メソッド要求](#oid-method-requests)または[oid セット要求](#oid-set-requests)で使用できます。

### <a href="" id="oid-method-requests"></a>OID\_NIC\_スイッチ\_VPORT\_パラメーターの OID メソッド要求の処理

それに関連するドライバーは oid\_NIC\_\_\_スイッチの OID メソッド要求を発行して、ネットワークアダプターの NIC スイッチに接続されている VPort の現在の構成パラメーターを照会します。 これまでのドライバーでは、vport [ **\_PARAMETERS 構造体\_vport\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)の**VPortId**メンバーを vport 識別子に設定することによって、照会する vport を指定しています。

NDIS では、OID\_NIC\_スイッチの OID メソッド要求を処理します。これは、ミニポートドライバーの VPORT\_パラメーター\_ます。 NDIS は、 [oid\_nic\_スイッチ](oid-nic-switch-create-vport.md)の前の oid 要求から取得した情報を返します。\_vport と[oid\_nic\_スイッチ\_列挙\_vport](oid-nic-switch-enum-vports.md)に\_作成します。

OID メソッド要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体へのポインターが含まれています。 この構造体には、指定されたスイッチの構成パラメーターが含まれています。

詳細については、「[仮想ポートのパラメーターのクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-virtual-port)」を参照してください。

### <a href="" id="oid-set-requests"></a>OID\_NIC\_スイッチ\_VPORT\_パラメーターの OID セット要求の処理

これまでのドライバーは、OID\_NIC\_スイッチの OID セット要求を発行して、VPORT\_パラメーター\_、ネットワークアダプターの NIC スイッチに接続されている VPort の現在の構成パラメーターを変更します。 この OID 要求を使用して、既定のパラメーターおよび既定以外の VPorts のパラメーターを更新できます。

VPort の構成パラメーターの一部だけを変更できます。 前のドライバーでは、 [**NDIS\_NIC\_スイッチ\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の次のメンバーを設定することによって、変更するパラメーターを指定します。

1.  **VPortId**メンバーは、パラメーターが変更される vport の識別子に設定されます。

2.  適切な NDIS\_NIC\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_変更したフラグが**フラグ**メンバーで設定されます。 [**Ndis\_nic\_スイッチ\_VPORT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体のメンバーは、対応する NDIS\_NIC\_スイッチ\_パラメーター\_*Xxx*\_changed フラグが Ntddndis で定義されている場合にのみ変更できます。

3.  [**NDIS\_NIC\_スイッチ\_vport\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の対応するメンバーには、変更する vport 構成パラメーターが設定されています。

PF ミニポートドライバーが oid\_NIC の OID セット要求を受信した後、VPORT\_パラメーター\_\_スイッチは、構成パラメーターを使用してハードウェアを構成します。 ドライバーは、NDIS\_NIC\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_変更されたフラグを変更することができます。これらの構成パラメーターは、 [**ndis\_NIC\_スイッチ\_VPORT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の**flags**メンバーにあります。

詳細については、「[仮想ポートのパラメーターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-virtual-port)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS または PF ミニポートドライバーは、OID\_NIC\_スイッチ\_VPORT\_パラメーターの設定またはメソッド OID 要求について、次のステータスコードを返します。

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
<td><p>要求は正常に完了しました。 <strong>Informationbuffer</strong>は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF ミニポートドライバーは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS または PF ミニポートドライバーは、データを設定し<strong>ます。METHOD_INFORMATION。BytesNeeded な</strong>メンバー (OID メソッド要求の場合) または<strong>データ。SET_INFORMATION。</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の bytesneeded メンバー (OID セット要求の場合) が、必要な最小バッファーサイズに設定されている必要があります。</p></td>
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
[**NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_スイッチ\_列挙型\_VPORTS](oid-nic-switch-enum-vports.md)

 

 




