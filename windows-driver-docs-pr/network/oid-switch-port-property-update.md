---
title: OID_SWITCH_PORT_PROPERTY_UPDATE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートポリシーのプロパティの更新について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PORT_PROPERTY_UPDATE に発行します。
ms.assetid: 674CA5EB-BF11-47E8-A2AC-6C789CA4FDB5
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_PORT_PROPERTY_UPDATE
ms.localizationpriority: medium
ms.openlocfilehash: 7b5afb7fa0c236c97d84cf5198ae2843ad859bf8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843925"
---
# <a name="oid_switch_port_property_update"></a>OID\_スイッチ\_ポート\_プロパティ\_更新


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_ポート\_プロパティ\_UPDATE によって、拡張可能なスイッチポートポリシーのプロパティの更新について拡張可能スイッチ拡張機能に通知します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   ポートプロパティの識別と種類を指定する、 [ **\_ポート\_プロパティ\_パラメーター構造の NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)。

-   ポートポリシーのパラメーターを格納しているプロパティバッファー。 プロパティバッファーには、 [**NDIS\_スイッチ\_PORT\_\_property**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)構造体の**PropertyType**メンバーに基づく構造体が含まれています。 たとえば、 **PropertyType**メンバーが**NdisSwitchPortPropertyTypeVlan**に設定されている場合、プロパティバッファーには、 [**NDIS\_スイッチ\_ポート\_プロパティ\_VLAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)構造が格納されます。

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID\_スイッチ\_ポート\_プロパティ\_更新の OID セット要求を処理できます。 その他のすべての種類の拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックの次の拡張機能に OID 要求を転送する必要があります。

拡張機能は、OID 要求に対して\_受け入れられない\_データ\_NDIS\_状態を返すことによって、ポートプロパティの更新を拒否することができます。 たとえば、拡張機能が、更新されたポリシーをポートに適用するためにリソースを割り当てることができない場合、更新要求を拒否する必要があります。

**注**  拡張機能が他の NDIS\_ステータス\_*Xxx*エラー状態コードを返す場合は、更新通知も拒否されます。 ただし、NDIS\_STATUS\_リソースを返すなど、一時的なシナリオのステータスコードを返すと、作成通知の再試行が発生する可能性があります。

 

拡張機能が OID 要求を拒否しない場合は、要求が完了したときに状態を監視する必要があります。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断するために、この処理を実行します。

Oid の OID セット要求を処理する方法に関するガイドラインについては\_\_ポート\_プロパティ\_更新については、「[ポートポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-port-policies)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

転送拡張機能が oid の OID セット要求を完了すると、\_ポート\_プロパティ\_更新\_、次のステータスコードのいずれかが返されます。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが小さすぎて、構造体のプロパティバッファー内の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PROPERTY_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)"><strong>NDIS_SWITCH_PORT_PROPERTY_PARAMETERS</strong></a>構造とデータを処理できません。 拡張機能はデータを設定し<strong>ます。SET_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>転送拡張機能がポートポリシーの削除通知を拒否しました。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>転送拡張機能は、ポートポリシーをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>OID 要求は、他の理由で失敗しました。</p></td>
</tr>
</tbody>
</table>

 

拡張機能が oid の OID 設定要求を完了していない場合\_\_ポート\_プロパティ\_更新の場合、要求は拡張可能スイッチの基になるミニポートエッジによって完了します。 ミニポートエッジは、次の状態コードを返します。

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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_ポート\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_custom)

[**NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)

[**NDIS\_スイッチ\_ポート\_プロパティ\_VLAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




