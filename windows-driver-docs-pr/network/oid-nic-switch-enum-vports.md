---
title: OID_NIC_SWITCH_ENUM_VPORTS
description: 前のドライバーまたはユーザーモードアプリケーションが、配列を取得するために OID_NIC_SWITCH_ENUM_VPORTS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 4B9587E0-3CA9-46AF-A80E-969E6D563922
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_ENUM_VPORTS
ms.localizationpriority: medium
ms.openlocfilehash: 612f5be262fbd7960ec2da9cd43970d7843b48fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844085"
---
# <a name="oid_nic_switch_enum_vports"></a>OID\_NIC\_スイッチ\_列挙型\_VPORTS


前のドライバーまたはユーザーモードのアプリケーションは、OID\_NIC\_スイッチのオブジェクト識別子 (OID) メソッド要求を発行して、配列を取得するために、列挙型\_VPORTS を\_します。 配列の各要素は、ネットワークアダプターの NIC スイッチで作成された仮想ポート (VPort) の属性を指定します。

この OID クエリ要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_VPORT\_INFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)配列内の要素の数を定義する配列構造体です。

-   [**NDIS\_NIC\_スイッチ\_VPORT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体の配列。 これらの各構造体には、ネットワークアダプターの NIC スイッチの VPort に関する情報が含まれています。

    **注**  ネットワークアダプターに vports が作成されていない場合、ドライバーは[**ndis\_NIC\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)の**numelements**メンバーを0に設定し、 [**NDIS\_NIC\_スイッチ\_vports\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体が返されます。\_\_

     

<a name="remarks"></a>注釈
-------

それ以降のドライバーやユーザーモードアプリケーションは OID\_\_NIC の OID クエリ要求を発行し、列挙型\_VPORTS によってネットワークアダプターの NIC スイッチに割り当てられている VPorts を列挙\_ます。

ドライバーまたはアプリケーションが OID 要求を発行する前に、要求と共に渡される、 [**VPORT\_INFO\_配列の構造\_、NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)を初期化する必要があります。 **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**構造体を初期化するときは、ドライバーまたはアプリケーションが次のガイドラインに従う必要があります。

-   NDIS\_NIC\_スイッチ\_VPORT\_INFO\_ARRAY\_特定の\_スイッチフラグが**Flags**メンバーで設定されている場合は、指定された NIC スイッチで作成されたすべての vport に関する情報が返されます。\_\_ NIC スイッチは、その構造体の**Switchid**メンバーによって指定されます。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプターの既定の NIC スイッチのみをサポートしています。 **Flags**メンバーで設定されているフラグに関係なく、 **SWITCHID**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

     

-   NDIS\_NIC\_スイッチ\_VPORT\_INFO\_ARRAY\_特定の\_関数フラグが**Flags**メンバーで設定されている場合は、ネットワークアダプターの指定された PCI Express (PCIe) 物理機能 (PF) または仮想関数 (VF) に接続されているすべての vport について情報が返されます。\_\_ PF または VF は、その構造体の**AttachedFunctionId**メンバーによって指定されます。

    **AttachedFunctionId**メンバーが NDIS\_PF\_関数\_ID に設定されている場合、ネットワークアダプターの pf に接続されているすべての vports (既定の vports を含む) に関する情報が返されます。 **AttachedFunctionId**メンバーが有効な vf 識別子に設定されている場合は、指定された vf のすべての vports に関する情報が返されます。

    **注**  Windows Server 2012 以降では、VF にアタッチできる既定以外の vport は1つだけです。 ただし、複数の VPorts (既定の Vports を含む) を PF に接続することはできます。

     

-   **Flags**メンバーが0に設定されている場合、ネットワークアダプターの PF または VF に接続されているすべての vports に関する情報が返されます。 この場合、 **Switchid**と**AttachedFunctionId**の値は無視されます。

詳細については、「[ネットワークアダプターの仮想ポートを列挙する](https://docs.microsoft.com/windows-hardware/drivers/network/enumerating-virtual-ports-on-a-network-adapter)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID\_NIC\_スイッチの OID メソッド要求を処理し\_列挙型\_VPORTS がミニポートドライバーに要求します。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_\_NIC を処理するときに、列挙型\_VPORTS の要求\_、次のステータスコードのいずれかが返されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"><strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[**NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)

[**NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_パラメーター](oid-nic-switch-parameters.md)

 

 




