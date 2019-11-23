---
title: OID_SWITCH_PARAMETERS
description: Hyper-v 拡張可能スイッチ拡張機能は、拡張可能なスイッチの構成データを取得するために、OID_SWITCH_PARAMETERS のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: F2CA0BE5-ED21-4ACF-B26A-4F512D4B15C7
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: d14c6e4dcdb57d21ecab84906d566232c70021be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843943"
---
# <a name="oid_switch_parameters"></a>OID\_スイッチ\_パラメーター


Hyper-v 拡張可能スイッチ拡張機能は、OID のオブジェクト識別子 (OID) クエリ要求を発行して、拡張可能なスイッチの構成データを取得するために、\_パラメーター\_切り替えます。

OID クエリ要求が正常に完了した場合、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

返された[**ndis\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造体を拡張して処理するときに、 **NDIS\_\_スイッチ**のさまざまな文字列メンバー ( **switchname**など) が null で終わると想定してはいけません。 これらの文字列メンバーのデータ型は、で[**文字列構造\_カウントされる\_場合**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)に、によって型定義されます。 拡張機能は、この構造体の**length**メンバーの値から文字列の長さを決定する必要があります。

**注**  文字列が null で終わる場合は、**長さ**のメンバーに終端の null 文字を含めることはできません。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID の OID クエリ要求を完了し\_パラメーターを\_し、次のステータスコードのいずれかを返します。

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
<td><p>情報バッファーの長さが小さすぎて、OID クエリ要求の OID_SWITCH_PARAMETERS 構造を返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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

[**NDIS\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




