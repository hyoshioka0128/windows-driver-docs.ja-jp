---
title: OID_SWITCH_NIC_CONNECT
description: HYPER-V 拡張可能なプロトコル edge スイッチのオブジェクト識別子 (OID) の設定、拡張可能スイッチ ポートとネットワーク アダプター間のネットワーク接続が拡張可能スイッチの拡張機能を基になるかを通知する OID_SWITCH_NIC_CONNECT の要求の問題完全に確立されます。 プロトコルのエッジは、以前に通知 OID_SWITCH_NIC_CREATE の OID セットの要求が発行されたときに拡張機能をこの接続が確立されています。
ms.assetid: 98A4AD28-2716-40DD-AE46-70969A23FAB7
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_CONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0a5a9a95aa1390d530160326764507d6bd086a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536853"
---
# <a name="oidswitchnicconnect"></a>OID\_スイッチ\_NIC\_接続


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_拡張可能スイッチの拡張機能を基になる通知への接続を間にネットワーク接続、拡張可能スイッチのポートおよびネットワーク アダプターが完全に確立します。 この接続されているプロトコルの以前に通知する edge 拡張機能では、OID セットの要求が発行されたときに確立されている[OID\_スイッチ\_NIC\_作成](oid-switch-nic-create.md)です。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_切り替える\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造の拡張可能スイッチのポートを指定しますこの接続の通知が行わします。 拡張可能スイッチ拡張機能は、次の方法でパラメーターについては、このポートおよびその他の拡張可能スイッチのポートを取得できます。

-   クエリの要求の OID を発行して[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)します。 拡張機能の問題この OID [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)場合にのみ OID\_スイッチ\_パラメーターを返します、 [ **NDIS\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598220)構造体**IsActive**を TRUE に設定します。 場合**IsActive** OID は、FALSE、拡張機能の問題は、ときに、 **NetEventSwitchActivate** [ **NET\_PNP\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff568751)拡張機能のミニポート アダプターによって発行されます。

-   さまざまな OID の要求の設定を調べることによって[OID\_スイッチ\_ポート\_作成](oid-switch-port-create.md)と[OID\_スイッチ\_ポート\_の削除](oid-switch-port-delete.md).

**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体は、ネットワーク アダプターのインデックスを指定します。対象の接続の通知が行われました。 指定したネットワーク アダプター**インデックス**値がで指定された拡張可能スイッチ ポートに接続されている、 **PortId**メンバー。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://msdn.microsoft.com/library/windows/hardware/hh598258)します。

OID の OID のセット要求を受け取ったとき\_スイッチ\_NIC\_接続で、拡張機能には、次のガイドラインが従う必要があります。

-   ときに OID\_スイッチ\_NIC\_NDIS との接続要求が完了した\_状態\_成功した場合、ネットワーク接続および拡張可能スイッチ ポートが完全に動作します。 拡張機能では、生成したり、ポートのネットワーク接続にパケット トラフィックを転送することができます。 拡張機能は、拡張可能スイッチ Oid または発信元ポートとしてポートを使用して、状態インジケーターを発行することもできます。 拡張機能を呼び出すことも[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)ポートの拡張可能スイッチの参照カウンターをインクリメントします。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215) OID 要求に関連付けられている構造体。

-   拡張機能は常に呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)基になる拡張機能には、この OID 要求を転送します。 拡張機能は、自体 OID 要求を完了する必要があります。

-   拡張可能スイッチの外部ネットワーク アダプターは、1 つまたは複数の基になる物理アダプターにバインドできます。 拡張可能スイッチのプロトコルのエッジが OID の独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべての物理ネットワーク アダプターの\_切り替える\_NIC\_接続します。 各 OID セットの要求では、別のネットワーク アダプター接続のインデックス値を指定します。 これらの値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://msdn.microsoft.com/library/windows/hardware/hh598258)します。

    拡張機能では、外部ネットワーク アダプターにバインドされている基になる各物理アダプターの接続状態を維持する必要があります。 外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](https://msdn.microsoft.com/library/windows/hardware/hh582274)します。

**注**  、拡張機能は、OID の独自の OID セット要求を発行する必要があります\_スイッチ\_NIC\_接続します。

 

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のセットの要求が完了すると\_切り替える\_NIC\_接続し、次のステータス コードを返します。

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
[**NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_スイッチ\_NIC\_を作成します。](oid-switch-nic-create.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 




