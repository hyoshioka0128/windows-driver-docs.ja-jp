---
title: OID_SWITCH_PORT_TEARDOWN
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの要求を発行し、拡張可能なスイッチの拡張機能が削除プロセスを開始することを OID_SWITCH_PORT_TEARDOWN に通知します。
ms.assetid: 94FA23AC-2064-40C8-B99C-D8D3DC10BFF9
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_TEARDOWN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 34e0375582c8ca1193cc19515985d1b8d77da67f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843923"
---
# <a name="oid_switch_port_teardown"></a>OID\_スイッチ\_ポート\_破棄


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの OID\_\_\_の要求を発行します。これにより、拡張可能なスイッチポートによって削除が開始される、基になる拡張可能なスイッチ拡張機能に通知します。process. このプロセスは、プロトコルドライバーが oid セットの oid 要求を発行すると、 [\_スイッチ\_ポート\_削除](oid-switch-port-delete.md)されると開始されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_PORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_port\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体の**ポート id**メンバーは、接続通知を行う拡張可能なスイッチポートを指定します。 拡張可能なスイッチ拡張機能は、次の方法で取得したポートに関するキャッシュされた情報を更新する必要があります。

-   Oid の OID クエリ要求を発行することによって[\_\_ポート\_配列に切り替え](oid-switch-port-array.md)ます。 拡張機能は、 [oid\_スイッチ\_パラメーター](oid-switch-parameters.md)が、 **IsActive**が TRUE に設定された[**NDIS\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造を返す場合にのみ、この oid を[*filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)に発行します。 **IsActive**が FALSE の場合、拡張機能のミニポートによって**NETEVENTSWITCHACTIVATE** [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)が発行されると、拡張機能は OID を発行します。

-   Oid のさまざまな OID セット要求を検査することによって[\_\_ポート\_作成](oid-switch-port-create.md)および[oid\_スイッチ\_ポート\_削除](oid-switch-port-delete.md)します。

拡張可能スイッチのプロトコルエッジは、\_ポート\_破棄\_の oid セット要求を発行し、拡張可能スイッチからポートが削除されていることを拡張機能に通知します。 この OID 要求が発行される前に、ポートにアクティブなネットワークアダプター接続がある場合は、拡張スイッチのプロトコルエッジで以前に次の Oid が発行されています。

-   [OID\_スイッチ\_NIC\_切断](oid-switch-nic-disconnect.md)。これにより、ネットワークアダプターが NDIS\_スイッチで指定されているポートに接続されなくなったことが、基になる拡張機能に通知され[ **\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)データ.

-   [OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)。ネットワークアダプターと拡張可能なスイッチポートの間のネットワーク接続が削除されたことを基になる拡張機能に通知します。

    プロトコルエッジは、指定された拡張可能なスイッチポートのすべての保留中パケットが取り消されたか、完了した後に、この OID セット要求を発行します。

拡張機能がこの OID セット要求を完了し、拡張可能なスイッチポートの参照カウンターがゼロの場合、拡張可能スイッチのプロトコルエッジは oid セット要求[\_ポート\_スイッチ](oid-switch-port-delete.md)を発行し、削除\_ます。 この OID 要求は、拡張可能なスイッチからポートを削除します。

拡張機能によって、参照可能なスイッチポートの参照カウンターがインクリメントさ  、参照可能[*Chport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)が呼び出されることに**注意**してください。 拡張機能は、 [*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)を呼び出すことによって参照カウンターをデクリメントします。

 

拡張機能は、OID の OID セット要求を処理するために、次のガイドラインに従う必要があります\_スイッチ\_ポート\_破棄します。

-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を失敗させることはできません。

    拡張機能では、OID 要求に関連付けられている[ **\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)の構造を変更**することは**できません  。

     

-   拡張機能がこの OID 要求を転送した後、削除されたポートにパケットを転送することはできません。 また、この拡張機能では、OID 要求を発行したり、削除されたポートに対して、[*この関数を使用したり*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)することはできません。

拡張機能では、OID の OID セット要求を発行する必要がありませ**ん  \_** スイッチ\_ポート\_破棄します。

 

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_ポート\_破棄の OID セット要求を完了し、次のステータスコードを返します。

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

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_パラメーター](oid-switch-parameters.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




