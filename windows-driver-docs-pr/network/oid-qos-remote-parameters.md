---
title: OID_QOS_REMOTE_PARAMETERS
description: このドライバーは、リモートピアの NDIS Quality of Service (QoS) パラメーターを取得するために、OID_QOS_REMOTE_PARAMETERS のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: F9DA87FF-577F-4E06-929B-4AD65105B2F0
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_QOS_REMOTE_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: 4b2ded1c4f44ccea3969828ff7aa0138e6d53724
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844024"
---
# <a name="oid_qos_remote_parameters"></a>OID\_QOS\_リモート\_パラメーター


このドライバーは、リモートピアの NDIS Quality of Service (QoS) パラメーターを取得するために、OID\_QOS\_リモート\_パラメーターのオブジェクト識別子 (OID) クエリ要求を発行します。 ミニポートドライバーは、これらのリモート QoS パラメーターを使用して、動作している NDIS QoS パラメーターを解決します。 ドライバーは、QoS パケット転送を実行するために、ネットワークアダプターに操作パラメーターを構成します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターが含まれています。

この OID クエリ要求  は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバーに対してのみ有効である**ことに注意**してください。

 

<a name="remarks"></a>注釈
-------

NDIS が\_OID の OID 要求を処理するときに、\_リモート\_パラメーターが正常に処理された場合は、以前の[**ndis\_ステータス\_qos\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)からキャッシュしていたリモート NDIS QOS パラメーターを返します。これは、ミニポートドライバーによって発行された\_変更の状態を示します。 ドライバーは、この状態の通知を発行して、リモート NDIS QoS パラメーターの初期セットを報告します。 また、このドライバーは、リモート NDIS QoS パラメーターが変更されるたびに、この状態を示します。

NDIS は、次の方法で初期化される[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を返します。

-   ミニポートドライバーによって以前に Ndis\_の状態が発行された場合は[ **\_qos\_リモート\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)の状態を示します。 Ndis は[**ndis\_QOS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)\_のパラメーターデータをキャッシュし、OID\_QOS\_リモート\_パラメーターの oid クエリ要求に対してこのデータを返します。

-   ミニポートドライバーが[**ndis\_status\_QOS\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行していない場合\_変更状態を示す\_、ndis は、すべてのメンバー (**ヘッダー**メンバーを除く) を0に設定して、 [**ndis\_QOS PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を返します。

リモート NDIS QoS パラメーターの詳細については、「 [Ndis Qos パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)」を参照してください。

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
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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

 

 




