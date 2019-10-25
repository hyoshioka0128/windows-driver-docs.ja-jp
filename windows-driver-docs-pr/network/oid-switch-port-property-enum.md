---
title: OID_SWITCH_PORT_PROPERTY_ENUM
description: Hyper-v 拡張可能スイッチ拡張機能は、配列を取得するために、OID_SWITCH_PORT_PROPERTY_ENUM のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 5C391B82-FCA6-4A95-992F-EDB5DF6183C7
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_PROPERTY_ENUM ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 801b7a5116d7dad1280ba71368abc363da8f3e4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843928"
---
# <a name="oid_switch_port_property_enum"></a>OID\_スイッチ\_ポート\_プロパティ\_列挙型


Hyper-v 拡張可能スイッチ拡張機能は、OID のオブジェクト識別子 (OID) メソッドの要求を発行し\_スイッチ\_ポート\_プロパティ\_列挙型を取得して、配列を取得します。 この配列には、指定した条件に一致するプロビジョニング済みポートポリシーが含まれています。 配列の各要素は、指定された拡張可能なスイッチポートのポリシーのプロパティを指定します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   指定されたポートのポリシー列挙のパラメーターを指定する[ **\_ポート\_プロパティ\_\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)。

-   [**NDIS\_スイッチの配列\_ポート\_プロパティ\_列挙型\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)構造体です。 これらの各構造体には、拡張可能なスイッチポートポリシーのプロパティに関する情報が含まれています。

    **注**  Ndis の**numproperties**メンバー [ **\_switch\_PORT\_プロパティ\_ENUM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)構造体が0に設定されている場合は、 [**ndis\_スイッチ\_ポートはありません\_プロパティ\_列挙型\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

Oid の OID メソッド要求を発行する前に、\_スイッチ\_ポート\_プロパティ\_列挙型では、拡張可能なスイッチ拡張機能は次のガイドラインに従う必要があります。

-   拡張機能は、拡張可能なスイッチのプロトコルエッジが[oid\_スイッチ\_ポート\_作成](oid-switch-port-create.md)要求を発行した後、\_ポート\_プロパティを発行するために、OID\_スイッチの\_プロパティを[OID\_\_ポート\_破棄](oid-switch-port-teardown.md)要求に切り替えます。

-   拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して OID\_スイッチ\_ポート\_プロパティ\_ENUM 要求に対して発行する前に、[*を呼び出す*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)必要があります。 これにより、OID 要求が完了するまで、指定したポートは削除されません。

    OID 要求の完了後、拡張機能は[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)を呼び出す必要があります。 この拡張機能は、OID 要求が NDIS\_STATUS\_SUCCESS で完了したかどうかに関係なく、この関数を呼び出す必要があります。

OID\_スイッチ\_ポート\_プロパティ\_ENUM OID は、Hyper-v 拡張スイッチでアクティブ化が完了している場合にのみ発行する必要があります。 詳細について[は、「Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)」を参照してください。

**注:** 拡張機能が OID の oid メソッド要求を受信した場合  \_スイッチ\_ポート\_プロパティ\_列挙型である場合、oid 要求を完了することはできません。 代わりに、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックで OID 要求を転送する必要があります。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID の OID クエリ要求を完了します。\_スイッチ\_ポート\_プロパティ\_列挙し、次のステータスコードを返します。

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
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_ポート\_プロパティ\_列挙型\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)

[**NDIS\_スイッチ\_ポート\_プロパティ\_列挙型\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




