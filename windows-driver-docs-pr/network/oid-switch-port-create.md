---
title: OID_SWITCH_PORT_CREATE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートの作成について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PORT_CREATE に発行します。
ms.assetid: 579D51CD-0594-4A06-998E-3886E7325D97
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_CREATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 4c72c4e09af8f2bc6aa2de2319a69fa111cd9d13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843937"
---
# <a name="oid_switch_port_create"></a>OID\_スイッチ\_ポート\_作成


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_\_ポートが作成され、拡張可能なスイッチポートの作成に関する拡張可能なスイッチ拡張機能が通知されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_PORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_port\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体の**ポート id**メンバーは、作成通知を行うポートを指定します。

拡張可能なスイッチ拡張機能では、次のガイドラインに従って、OID の OID セット要求を処理する必要があります\_スイッチ\_ポート\_作成します。

-   拡張機能では、OID 要求に関連付けられている[**ポート\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)を変更することはできません。

-   拡張機能は、OID 要求に対して\_受け入れられていない\_データ\_NDIS\_状態を返すことによって、作成通知を拒否できます。 たとえば、拡張機能が、そのポートで構成されたポリシーを適用するためにリソースを割り当てることができない場合、ドライバーは作成通知を拒否する必要があります。

    拡張機能が他の NDIS\_ステータス\_*Xxx*エラー状態コードを返す場合、作成通知も拒否されます。 ただし、NDIS\_STATUS\_リソースを返すなど、一時的なシナリオのステータスコードを返すと、作成通知の再試行が発生する可能性があります。

    拡張機能が OID 要求を拒否しない場合は、要求が完了したときに状態を監視する必要があります。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断するために、この処理を実行します。

    ポートポリシーの詳細については、「 [Hyper-v 拡張可能スイッチポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-hyper-v-extensible-switch-extensibility-policies)」を参照してください。

-   この OID セット要求を転送するために拡張機能が[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す場合、拡張機能はこの oid 要求の完了状態を監視する必要があります。 拡張機能は、拡張可能なスイッチドライバースタック内の基になる拡張機能がポート作成通知を拒否したかどうかを検出します。

-   OID 要求が転送され、正常に完了すると、拡張機能は、oid\_SWITCH の OID 要求が発生するまで、 [oid\_スイッチ\_ポート\_プロパティ\_列挙型](oid-switch-port-property-enum.md)などの、ポートに対する oid 要求を発行でき[\_破棄](oid-switch-port-teardown.md)が発行さ\_ポート。 この OID 要求は、ポートが拡張可能スイッチから削除プロセスを開始することを拡張機能に通知します。

-   拡張機能は、 [**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造の指定されたポートにパケットを転送することができません。 [oid\_スイッチ\_NIC](oid-switch-nic-connect.md)の設定要求が実行され、接続が完了します。なく.

**注**  拡張機能では、OID の oid セット要求を発行しないでください\_スイッチ\_ポート\_作成します。

 

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張機能が oid の OID セット要求を完了すると、\_スイッチ\_ポートの作成\_、次のステータスコードのいずれかが返されます。

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
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>拡張機能は作成通知を拒否します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>リソースの状態が低いため、この拡張機能は作成通知を拒否します。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>この拡張機能は、その他の理由で作成通知を拒否します。</p></td>
</tr>
</tbody>
</table>

 

**注**  は、拡張機能が OID セット要求を完了した場合、NDIS\_STATUS\_SUCCESS を返さないようにする必要があります。

 

拡張機能が oid の OID 設定要求を完了していない場合は\_\_ポートの作成\_作成、拡張スイッチの基になるミニポートエッジによって要求が完了します。 基になるミニポートエッジは、この OID セット要求に対して次の状態コードを返します。

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

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[OID\_スイッチ\_ポート\_プロパティ\_列挙型](oid-switch-port-property-enum.md)

 

 




