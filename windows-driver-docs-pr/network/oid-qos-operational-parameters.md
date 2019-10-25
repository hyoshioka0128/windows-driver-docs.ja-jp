---
title: OID_QOS_OPERATIONAL_PARAMETERS
description: このドライバーは、ネットワークアダプターの現在の NDIS Quality of Service (QoS) 操作パラメーターを取得するために、OID_QOS_OPERATIONAL_PARAMETERS のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 546EE7C6-BCED-4FF9-9B87-A36199B1B31C
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_QOS_OPERATIONAL_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c3ad5bdcaa1ae8bfc5d11d09f2316f3bfee3d829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844027"
---
# <a name="oid_qos_operational_parameters"></a>OID\_QOS\_操作\_パラメーター


ネットワークアダプターの現在の NDIS Quality of Service (QoS) 操作パラメーターを取得するために、後のドライバーが OID\_QOS\_操作\_パラメーターのオブジェクト識別子 (OID) クエリ要求を発行します。 ミニポートドライバーは、QoS パケット転送を実行するために、運用 NDIS QoS パラメーターを使用してネットワークアダプターを構成します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターが含まれています。

この OID クエリ要求は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバー用に NDIS によって処理される  に**注意**してください。

 

<a name="remarks"></a>注釈
-------

NDIS は、OID の oid クエリ要求を処理するときに、\_QOS\_操作\_パラメーターを正常に処理した後、以前の\_Ndis からキャッシュされた operational NDIS QoS パラメーターを返し\_[**qos\_操作\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change) 、ミニポートドライバーによって発行された状態の表示を変更します。 ドライバーは、この状態の通知を発行して、運用 NDIS QoS パラメーターの初期セットを報告します。 また、このドライバーは、運用 NDIS QoS パラメーターが変更されるたびに、この状態を示します。

NDIS は、次の方法で初期化される[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を返します。

-   ミニポートドライバーによって以前に Ndis\_の状態が発行された場合は[ **\_qos\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)の状態を示しています。 ndis は、 [**ndis\_QOS\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)データをキャッシュし、これを返します。OID\_QOS\_操作\_パラメーターの OID クエリ要求のデータ。

-   ミニポートドライバーが[**ndis\_状態\_QOS\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行しなかった場合\_変更の状態を示す\_[ **、ndis は**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)、すべてのメンバー (**ヘッダー**メンバーを除く) は0に設定されます。

運用 NDIS QoS パラメーターの詳細については、「 [Ndis Qos パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、次のいずれかの状態コードを返します。

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
<td><p>ミニポートドライバーは、NDIS QoS インターフェイスをサポートしていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="even">
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
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS\_ステータス\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)

[**NDIS\_ステータス\_QOS\_リモート\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)

[OID\_QOS\_パラメーター](oid-qos-parameters.md)

 

 




