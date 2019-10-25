---
title: OID_SWITCH_PORT_FEATURE_STATUS_QUERY
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートに関する拡張機能からカスタムステータス情報を取得するために、オブジェクト識別子 (OID) メソッドの OID_SWITCH_PORT_FEATURE_STATUS_QUERY 要求を発行します。
ms.assetid: 577CF1C2-9737-4FB0-9C40-AEE529EF1439
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_FEATURE_STATUS_QUERY ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a3ec424d3e9451c56ba669d170dba9392c325aca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843933"
---
# <a name="oid_switch_port_feature_status_query"></a>OID\_スイッチ\_ポート\_機能\_状態\_クエリ


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) のメソッドの要求 OID\_スイッチ\_ポート\_機能\_ステータス\_クエリを発行して、拡張機能からカスタムステータス情報を取得します。拡張可能なスイッチポート。 この情報は、*機能の状態*情報として知られています。 この情報の形式は、独立系ソフトウェアベンダー (ISV) によって定義されます。

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [**NDIS\_スイッチ\_ポート\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)構造で、返される機能ステータス情報の種類のパラメーターを指定します。

-   [**NDIS\_スイッチ\_ポート\_機能\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom) 、拡張可能なスイッチポートの機能状態情報を含むカスタム構造ます。

<a name="remarks"></a>注釈
-------

Oid の OID セット要求を処理する方法に関するガイドラインについては\_スイッチ\_ポート\_機能\_状態\_クエリについては、「[カスタムポート機能の状態情報の管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-custom-port-feature-status-information)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

この拡張機能は、oid\_スイッチ\_ポート\_機能の OID メソッド要求について、次のいずれかの状態コードを返します\_状態\_クエリです。

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
<td><p>情報バッファーの長さが小さすぎて、機能の状態の情報だけでなく、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)"><strong>NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)"><strong>NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS</strong></a>構造体も返すことができません。 拡張可能スイッチの基になるミニポートエッジによってデータが設定され<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_スイッチ\_ポート\_機能\_状態\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)

[**NDIS\_スイッチ\_ポート\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)

[**NDIS\_スイッチ\_ポート\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)

 

 




