---
title: OID_SWITCH_FEATURE_STATUS_QUERY
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能スイッチに関する拡張機能からカスタムステータス情報を取得するために、オブジェクト識別子 (OID) メソッドの OID_SWITCH_FEATURE_STATUS_QUERY 要求を発行します。
ms.assetid: 580EFBD0-7798-4C56-99C5-84EADB8F8E82
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_FEATURE_STATUS_QUERY ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7165676f77980acf6c127891ed25629da7cacf27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843966"
---
# <a name="oid_switch_feature_status_query"></a>OID\_スイッチ\_機能\_状態\_クエリ


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) メソッドの OID\_スイッチ\_機能\_状態\_クエリを発行して、拡張可能スイッチに関する拡張機能からカスタムステータス情報を取得します。 この情報は、*機能の状態*情報として知られています。 この情報の形式は、独立系ソフトウェアベンダー (ISV) によって定義されます。

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   取得する機能ステータス情報の種類のパラメーターを指定する[**NDIS\_スイッチ\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)構造。

-   拡張可能なスイッチの機能の状態情報を格納している[**カスタム構造\_、NDIS\_スイッチ\_の状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom) 。

<a name="remarks"></a>注釈
-------

Oid の OID セット要求を処理する方法に関するガイドラインについては\_スイッチ\_機能\_状態\_クエリについては、「[カスタムスイッチ機能の状態情報の管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-custom-switch-feature-status-information)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張機能は、oid\_スイッチ\_機能\_状態\_クエリの OID メソッド要求について、次のいずれかの状態コードを返します。

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
<td><p>情報バッファーの長さが小さすぎて、機能の状態の情報だけでなく、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)"><strong>NDIS_SWITCH_FEATURE_STATUS_CUSTOM</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)"><strong>NDIS_SWITCH_FEATURE_STATUS_PARAMETERS</strong></a>構造体も返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_スイッチ\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)

[**NDIS\_スイッチ\_の機能\_状態\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)

[**NDIS\_スイッチ\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)

 

 




