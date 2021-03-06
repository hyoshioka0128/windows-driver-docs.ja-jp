---
title: OID_SWITCH_PORT_TEARDOWN
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチ ポートが削除プロセスを開始する基になる拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_TEARDOWN のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 94FA23AC-2064-40C8-B99C-D8D3DC10BFF9
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_TEARDOWN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5251c0d3f19f87352426c11c6050d852c5b5c93f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386983"
---
# <a name="oidswitchportteardown"></a>OID\_スイッチ\_ポート\_破棄


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_に、拡張可能スイッチのポートは拡張可能スイッチの拡張機能を基になる通知の破棄削除プロセスを開始します。 プロトコル ドライバーの OID セット要求を発行するときに、このプロセスが開始された[OID\_スイッチ\_ポート\_削除](oid-switch-port-delete.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_切り替える\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体は、拡張可能スイッチ ポートを指定します対象の接続の通知が行われました。 拡張可能スイッチ拡張機能は、次の方法で取得されるポートに関するキャッシュされた情報を更新する必要があります。

-   クエリの要求の OID を発行して[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)します。 拡張機能の問題この OID [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)場合にのみ[OID\_スイッチ\_パラメーター](oid-switch-parameters.md)を返します、 [ **NDIS\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造体**IsActive**を TRUE に設定します。 場合**IsActive** OID は、FALSE、拡張機能の問題は、ときに、 **NetEventSwitchActivate** [ **NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)拡張子ミニポートによって発行されます。

-   さまざまな OID の要求の設定を調べることによって[OID\_スイッチ\_ポート\_作成](oid-switch-port-create.md)と[OID\_スイッチ\_ポート\_の削除](oid-switch-port-delete.md).

OID の OID セット要求を発行する拡張可能スイッチのプロトコルの edge\_切り替える\_ポート\_拡張可能スイッチから削除中のポートである拡張機能への通知を破棄します。 この OID 要求が発行される前に、ポートがアクティブなネットワーク アダプターの接続がある場合、拡張可能スイッチのプロトコルのエッジは以前、次の Oid を発行しました。

-   [OID\_スイッチ\_NIC\_切断](oid-switch-nic-disconnect.md)で指定されているポートに接続されているネットワーク アダプターが不要の拡張機能を基になると通知する、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体。

-   [OID\_切り替える\_NIC\_削除](oid-switch-nic-delete.md)、ネットワーク アダプターと拡張可能スイッチのポート間のネットワーク接続が削除されている基になる拡張機能を通知します。

    プロトコルのエッジは、指定した拡張可能なスイッチ ポートの保留中のすべてのパケットがキャンセルまたは完了した後に、この OID のセット要求を発行します。

拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行、拡張機能がこの OID セット要求を完了するし、拡張可能スイッチ ポートの参照カウンターがゼロ、 [OID\_切り替える\_ポート\_削除](oid-switch-port-delete.md)します。 この OID 要求は、拡張可能スイッチのポートを削除します。

**注**  拡張機能は、呼び出すことによって拡張可能スイッチ ポートの参照カウンターをインクリメント[ *ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)します。 拡張機能をデクリメントを呼び出すことによって参照カウンター [ *DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)します。

 

拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_スイッチ\_ポート\_破棄。

-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

    **注**  、拡張機能は変更しないで、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)に関連付けられている構造体OID 要求。

     

-   後、拡張機能は、この OID 要求を転送する削除済みのポートにパケットを転送することはできません。 OID 要求も呼び出しに、拡張機能も発行できません、 [ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)削除済みのポートの関数。

**注**  、拡張機能は OID の OID のセット要求を発行する必要があります\_スイッチ\_ポート\_破棄します。

 

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のセットの要求が完了すると\_切り替える\_ポート\_破棄し、次のステータス コードを返します。

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
<td><p>OID 要求は正常に完了しました。</p></td>
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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_パラメーター](oid-switch-parameters.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




