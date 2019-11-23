---
title: OID_NIC_SWITCH_ENUM_SWITCHES
description: 前のドライバーまたはユーザーモードアプリケーションが、配列を取得するために OID_NIC_SWITCH_ENUM_SWITCHES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 706C3F1C-239F-4731-A38E-E150D26C79A5
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_ENUM_SWITCHES
ms.localizationpriority: medium
ms.openlocfilehash: ffa90622d033e4b862fbabe43236536cc8698878
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844090"
---
# <a name="oid_nic_switch_enum_switches"></a>OID\_NIC\_スイッチ\_列挙型\_スイッチ


それ以降のドライバーまたはユーザーモードアプリケーションは、OID\_NIC\_スイッチのオブジェクト識別子 (OID) クエリ要求を発行して、配列を取得するための列挙\_スイッチ\_します。 配列の各要素は、ネットワークアダプターで作成された NIC スイッチの属性を指定します。

この OID クエリ要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)内の要素の数を定義する配列構造体です。

-   \_情報構造体の[**NDIS\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)の配列。 これらの各構造体には、ネットワークアダプターで作成された1つの NIC スイッチに関する情報が含まれています。

    **注**  ネットワークアダプターに nic スイッチがない場合、ドライバーは、NDIS\_Nic の**numelements**メンバー [ **\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)構造体をゼロに設定し、 [**ndis\_NIC\_スイッチ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

その後のドライバーとユーザーモードアプリケーションは、OID\_\_NIC の OID クエリ要求を発行します。これにより、列挙型\_スイッチ\_、ネットワークアダプターで作成された NIC スイッチを列挙できます。

**注**  Windows Server 2012 以降では、シングルルート i/o 仮想化 (sr-iov) インターフェイスでは、ネットワークアダプターの既定の NIC スイッチのみがサポートされます。 このため、返される[**ndis\_nic\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)構造では、既定の nic スイッチに対して1つの[**ndis\_nic\_スイッチ\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)要素を指定する必要があります。これは、NDIS\_既定\_スイッチ\_ID の識別子によって参照されます。

 

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーの\_列挙\_スイッチ要求を使用して、OID\_NIC\_スイッチの OID クエリ要求を処理します。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_\_NIC を処理するときに、\_列挙型\_スイッチ要求では、次のいずれかの状態コードが返されます。

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
<td><p>ミニポートドライバーが SR-IOV インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_INFO_ARRAY</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[**NDIS\_NIC\_スイッチ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)

[**NDIS\_NIC\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_パラメーター](oid-nic-switch-parameters.md)

 

 




