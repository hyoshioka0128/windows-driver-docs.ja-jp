---
title: OID_SWITCH_NIC_ARRAY
description: Hyper-v 拡張可能スイッチ拡張機能は、配列を取得するために、OID_SWITCH_NIC_ARRAY のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: CA9958DF-4389-4B4F-B110-03F500E27A1B
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_NIC_ARRAY
ms.localizationpriority: medium
ms.openlocfilehash: 27da1486e86165a343a22643748c66223b76d4a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843963"
---
# <a name="oid_switch_nic_array"></a>OID\_スイッチ\_NIC\_配列


Hyper-v 拡張可能スイッチ拡張機能は、OID のオブジェクト識別子 (OID) クエリ要求を発行し、\_NIC\_配列を取得して配列を取得\_します。 配列の各要素は、拡張可能なスイッチポートに関連付けられている仮想ネットワークアダプターの構成パラメーターを指定します。

OID クエリ要求が正常に完了した場合、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれます。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_スイッチ\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)配列内の要素の数を定義する配列構造体です。 この構造体は、配列内の最初の要素へのオフセットも指定します。

-   [**NIC\_パラメーター構造体\_の NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)の配列。 これらの各構造体には、拡張可能なスイッチポートに接続されているネットワークアダプターに関する情報が含まれています。

    **注**  拡張スイッチポートに接続されているネットワークアダプターがない場合は、拡張可能スイッチの基になるミニポートエッジによって、NDIS\_スイッチの**numelements**メンバー [ **\_NIC\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)構造が0に設定されます。 この場合、 [**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体は返されません。

     

<a name="remarks"></a>注釈
-------

OID\_スイッチ\_NIC\_配列 OID は、Hyper-v 拡張スイッチでアクティブ化が完了している場合にのみ発行する必要があります。 詳細について[は、「Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)」を参照してください。

返された[**ndis\_スイッチ\_NIC\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体が拡張機能によって処理される場合、 [**ndis\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造 ( **NicFriendlyName**など) のさまざまな文字列メンバーが NULL で終わると想定しないでください。 これらの文字列メンバーのデータ型は、で[**文字列構造\_カウントされる\_場合**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)に、によって型定義されます。 ドライバーは、この構造体の**length**メンバーの値から文字列の長さを判断する必要があります。

**注**  文字列が null で終わる場合は、**長さ**のメンバーに終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_NIC\_配列の OID クエリ要求を完了し、次のステータスコードのいずれかを返します。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが小さすぎて、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)"><strong>NDIS_SWITCH_NIC_ARRAY</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)"><strong>NDIS_SWITCH_NIC_PARAMETERS</strong></a>要素の配列を返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_NIC\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)

[**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




