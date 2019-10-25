---
title: OID_SWITCH_PORT_DELETE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートの削除について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PORT_DELETE に発行します。
ms.assetid: D8893395-3D33-4777-B8F0-4DD6BE9B8A37
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_DELETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: cc6a6dc81687bc9eb29d8b2b27c26e751c312c67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843935"
---
# <a name="oid_switch_port_delete"></a>OID\_スイッチ\_ポートの削除\_


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_\_ポートが削除され、拡張可能なスイッチポートの削除に関する拡張可能なスイッチ拡張機能が通知されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_PORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_port\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体の**ポート id**メンバーは、削除通知を行う拡張可能なスイッチポートを指定します。

ネットワークアダプターが指定されたポートに接続されている場合、拡張可能スイッチのプロトコルエッジは、ポートを削除する前に接続を削除します。 この場合、プロトコルエッジはポートを削除する前に、次の手順に従います。

-   プロトコルエッジは oid セット要求[\_\_\_oid](oid-switch-nic-disconnect.md)を発行して、ネットワークアダプターと拡張可能なスイッチポートとの間の接続が削除中であることを拡張機能に通知します。

-   指定された拡張可能なスイッチポートのすべての保留中パケットが取り消されたか、完了すると、プロトコルエッジは oid セット要求を発行して、 [\_\_NIC](oid-switch-nic-delete.md)に対する接続を拡張に通知\_します。ネットワークアダプターと拡張可能なスイッチポートが削除されました。

    この時点で、プロトコルエッジはポートの削除を開始できます。

拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートを削除するときに、次の手順に従います。

1.  拡張可能スイッチのプロトコルエッジは、 [oid\_スイッチ\_ポート\_破棄](oid-switch-port-teardown.md)の oid セット要求を発行します。 この OID 要求は、拡張可能なスイッチポートの削除プロセスの開始について、基になる拡張可能なスイッチ拡張機能に通知します。

2.  プロトコルエッジは、拡張可能なスイッチポートに対するすべての OID 要求が完了した後に、oid\_スイッチ\_ポートの oid セット要求を発行して、削除\_ます。

    **注**  拡張機能が、ポートの参照カウンターをインクリメントするために参照として以前に[*参照を参照*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)していた場合は、プロトコルのエッジが OID を発行する前に[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)を呼び出す必要があり[\_スイッチ\_NIC\_の削除](oid-switch-nic-delete.md)要求です。

     

拡張機能は、次のガイドラインに従って、OID の OID セット要求を処理する必要があります\_スイッチ\_ポート\_削除します。

-   拡張機能では、OID 要求に関連付けられている[**ポート\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)を変更することはできません。

-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を失敗させることはできません。

-   OID\_スイッチ\_ポート\_DELETE 要求が NDIS\_STATUS\_SUCCESS で完了した後、拡張機能は削除されたポートに対してパケットまたは OID 要求を受信しません。 拡張機能は、削除されたポートにパケットを転送できません。 また、この拡張機能では、OID 要求を発行したり、削除されたポートに対して、[*この関数を使用したり*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)することはできません。

**注**拡張可能なスイッチ拡張機能  OID\_スイッチ\_ポート\_削除の oid セット要求を発行することはできません。

 

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、oid\_スイッチ\_ポートの OID セット要求を完了し\_削除して、次のステータスコードを返します。

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

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




