---
title: OID_SWITCH_PORT_DELETE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのポートの削除に関する拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_DELETE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: D8893395-3D33-4777-B8F0-4DD6BE9B8A37
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2b27ea56f2da65e215ebc7688e4926064acf3f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552959"
---
# <a name="oidswitchportdelete"></a>OID\_スイッチ\_ポート\_削除


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_拡張可能スイッチの拡張機能で拡張可能スイッチ ポートの削除についての通知を削除します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_切り替える\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体は、拡張可能スイッチ ポートを指定します対象の削除通知が行われました。

ネットワーク アダプターが、指定されたポートに接続されている、ポートを削除する前に、拡張可能スイッチのプロトコルのエッジは接続が削除されます。 ここでは、ポートを削除する前に、プロトコル エッジはこれらの手順に従いますは。

-   プロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_切断](oid-switch-nic-disconnect.md)にネットワーク アダプターと、拡張可能スイッチ ポート間の接続されている拡張機能を通知するには削除されます。

-   プロトコルのエッジがの OID セット要求を発行後、指定した拡張可能なスイッチ ポートのパケットの保留中のすべては、キャンセルまたは完了されていますが、 [OID\_切り替える\_NIC\_削除](oid-switch-nic-delete.md)に通知する、ネットワーク アダプターと、拡張可能スイッチ ポート間の接続が削除されている拡張機能。

    この時点では、プロトコルのエッジは、ポートの削除を開始できます。

拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのポートを削除するときに次の手順に従います。

1.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_破棄](oid-switch-port-teardown.md)します。 この OID 要求では、拡張可能スイッチ ポートの削除プロセスの開始に関する拡張可能スイッチの拡張機能を基になるに通知します。

2.  OID の OID セット要求を発行するプロトコル edge\_スイッチ\_ポート\_拡張可能スイッチ ポートにすべての OID 要求が完了した後に削除します。

    **注**  、拡張機能が呼び出されていた場合[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295) 、ポートの参照カウンターをインクリメントする呼び出す必要があります[ *DereferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598142)プロトコル エッジの問題の前に、 [OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)要求。

     

拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_スイッチ\_ポート\_を削除します。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229) OID 要求に関連付けられている構造体。

-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

-   OID 後\_スイッチ\_ポート\_NDIS 削除要求が完了しました\_状態\_成功すると、拡張機能は受け取りません任意パケットまたは削除済みのポートの OID 要求。 拡張機能は、削除済みのポートにパケットを転送できません。 OID 要求も呼び出しに、拡張機能も発行できません、 [ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)削除済みのポートの関数。

**注**  拡張可能スイッチの拡張機能は OID の OID のセット要求を発行する必要があります\_切り替える\_ポート\_を削除します。

 

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、[Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のセットの要求が完了すると\_切り替える\_ポート\_を削除し、次のステータス コードを返します。

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
[*DereferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598142)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598229)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 




