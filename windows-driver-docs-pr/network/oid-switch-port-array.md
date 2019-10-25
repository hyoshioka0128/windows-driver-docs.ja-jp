---
title: OID_SWITCH_PORT_ARRAY
description: Hyper-v 拡張可能スイッチ拡張機能は、OID_SWITCH_PORT_ARRAY のオブジェクト識別子 (OID) クエリ要求を発行して、配列を取得します。 配列の各要素は、拡張可能なスイッチポートの構成パラメーターを指定します。
ms.assetid: 9ED5E7A5-A23E-48E7-B8A2-9089C81851A1
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_ARRAY ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 62726f7a73eb82ccb946462f6343c73858830c47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843939"
---
# <a name="oid_switch_port_array"></a>OID\_スイッチ\_ポート\_配列


Hyper-v 拡張可能スイッチ拡張機能は、OID\_オブジェクト識別子 (OID) クエリ要求を発行して、配列\_ポート\_配列を取得します。 配列の各要素は、拡張可能なスイッチポートの構成パラメーターを指定します。

OID クエリ要求が正常に完了した場合、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれます。 このバッファーには、次のデータが含まれています。

-   配列内の要素の数を定義する[**NDIS\_スイッチ\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)構造体。

-   [**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)の構造体の配列。 これらの各構造体には、拡張可能スイッチのポートに関する情報が含まれています。

    **注**  拡張可能なスイッチにポートが作成されていない場合、ドライバーは、 [**ndis\_\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)の**numelements**メンバーを0に設定し、 [**ndis\_スイッチを設定しません\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造が返されます。

     

<a name="remarks"></a>注釈
-------

OID\_スイッチ\_ポート\_配列 OID は、Hyper-v 拡張スイッチでアクティブ化が完了している場合にのみ発行する必要があります。 詳細について[は、「Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)」を参照してください。

返された[**ndis\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)の構造体が拡張機能によって処理される場合、\_ndis のさまざまな文字列メンバーが **\_ポート\_パラメーター**構造を切り替えると想定しないでください。**PortName**として、は null で終了します。 これらの文字列メンバーのデータ型は、で[**文字列構造\_カウントされる\_場合**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)に、によって型定義されます。 ドライバーは、この構造体の**length**メンバーの値から文字列の長さを判断する必要があります。

**注**  文字列が null で終わる場合は、**長さ**のメンバーに終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_ポート\_配列の OID クエリ要求を完了し、次のステータスコードのいずれかを返します。

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
<td><p>情報バッファーの長さが小さすぎて、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)"><strong>NDIS_SWITCH_PORT_ARRAY</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)"><strong>NDIS_SWITCH_PORT_PARAMETERS</strong></a>要素の配列を返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_スイッチ\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




