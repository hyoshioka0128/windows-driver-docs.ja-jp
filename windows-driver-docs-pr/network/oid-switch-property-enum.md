---
title: OID_SWITCH_PROPERTY_ENUM
description: Hyper-v 拡張可能スイッチ拡張機能は、配列を取得するために、OID_SWITCH_PROPERTY_ENUM のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 45277355-4486-4CE0-ACBF-68D6BC6B79E7
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_PROPERTY_ENUM
ms.localizationpriority: medium
ms.openlocfilehash: 220b0885b9393d13853bd363bcfe93b529fdde4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843915"
---
# <a name="oid_switch_property_enum"></a>OID\_SWITCH\_プロパティ\_列挙型


Hyper-v 拡張可能スイッチ拡張機能は、OID のオブジェクト識別子 (OID) メソッドの要求を発行して、\_SWITCH\_プロパティ\_列挙型に配列を取得します。 この配列には、指定した条件に一致するプロビジョニング済みスイッチポリシーが含まれています。 配列の各要素は、拡張可能なスイッチポリシーのプロパティを指定します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_スイッチ\_プロパティ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters) 、拡張可能なスイッチポリシーの列挙のパラメーターを指定する列挙型\_パラメーター構造です。

-   [**ENUM\_INFO 構造体\_、NDIS\_SWITCH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)の配列。 これらの各構造体には、拡張可能なスイッチポリシーに関する情報が含まれています。

    **注:** 拡張機能が指定された拡張可能なスイッチポリシーのインスタンスを使用してプロビジョニングされていない場合は、拡張機能によって、 [**ndis\_SWITCH\_\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)の**numproperties**メンバーが0に設定され、 [**ndis\_switch\_プロパティ\_enum\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)構造体が返され  ます。\_

     

<a name="remarks"></a>注釈
-------

OID\_スイッチ\_プロパティ\_列挙型 OID は、Hyper-v 拡張スイッチでアクティブ化が完了している場合にのみ発行する必要があります。 詳細について[は、「Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)」を参照してください。

Oid の OID クエリ要求[\_スイッチ\_ポート\_プロパティ\_列挙型](oid-switch-port-property-enum.md)の場合とは異なり、拡張機能は、拡張可能なスイッチドライバースタックから、列挙型\_プロパティ\_列挙型要求を発行するときに、この*拡張機能を*呼び出す*必要はあり*ません。\_

**注:** 拡張機能が OID の oid メソッド要求を受け取った場合は  \_SWITCH\_プロパティ\_列挙型であるため、oid 要求を完了することはできません。 代わりに、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックで OID 要求を転送する必要があります。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_SWITCH\_プロパティ\_列挙型の OID クエリ要求を完了し、次のステータスコードのいずれかを返します。

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
<td><p>情報バッファーの長さが小さすぎて、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)"><strong>NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS</strong></a>構造体と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)"><strong>NDIS_SWITCH_PROPERTY_ENUM_INFO</strong></a>要素の配列を返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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

[**NDIS\_スイッチ\_プロパティ\_列挙型\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)

[**NDIS\_SWITCH\_プロパティ\_列挙型\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)

[Hyper-v 拡張可能スイッチ構成のクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




