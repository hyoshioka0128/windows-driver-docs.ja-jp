---
title: OID_SWITCH_PORT_ARRAY
description: HYPER-V 拡張可能なスイッチ、拡張機能の問題は、オブジェクト識別子 (OID) のクエリ要求を OID_SWITCH_PORT_ARRAY の配列を取得します。 配列内の各要素には、拡張可能スイッチ ポートの構成パラメーターを指定します。
ms.assetid: 9ED5E7A5-A23E-48E7-B8A2-9089C81851A1
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_ARRAY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3fb2c9d0837d812fef094895c2612c4a61efefde
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386855"
---
# <a name="oidswitchportarray"></a>OID\_スイッチ\_ポート\_配列


HYPER-V 拡張可能スイッチの拡張機能の OID オブジェクト識別子 (OID) のクエリ要求を発行する\_切り替える\_ポート\_配列が配列を取得します。 配列内の各要素には、拡張可能スイッチ ポートの構成パラメーターを指定します。

OID のクエリ要求が正常に完了した場合、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造が含まれていますバッファーへのポインター。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_array)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体。 各構造体には、拡張可能スイッチのポートに関する情報が含まれています。

    **注**  拡張可能スイッチのポートが作成されていない場合、ドライバーの設定、 **NumElements**のメンバー、 [ **NDIS\_切り替える\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_array)構造体を 0、no [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

OID\_切り替える\_ポート\_配列 OID は、HYPER-V 拡張可能スイッチには、アクティブ化が完了したときにのみ発行する必要があります。 参照してください[HYPER-V 拡張可能スイッチの構成を照会](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)の詳細。

拡張機能が、返されたは処理[ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造にする必要がありますわけでは、のメンバーの文字列、さまざまなこと**NDIS\_スイッチ\_ポート\_パラメーター**構造体など**PortName**null で終わるされます。 これらの文字列型のメンバーのデータ型は、型定義、 [**場合\_カウント済\_文字列**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)構造体。 ドライバーの値から文字列の長さを決定する必要があります、**長さ**この構造体のメンバー。

**注**  文字列が null で終わる場合、**長さ**メンバーは、終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_ポート\_配列と、次のステータス コードの 1 つを返します。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>返される情報バッファーの長さが小さすぎる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_array" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_array)"> <strong>NDIS_SWITCH_PORT_ARRAY</strong> </a>とその配列の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)"> <strong>NDIS_SWITCH_PORT_PARAMETERS</strong> </a>要素。 拡張可能スイッチのセットの基になるミニポート edge、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_array)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[HYPER-V 拡張可能スイッチの構成のクエリを実行します。](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




