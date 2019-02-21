---
title: OID_SWITCH_PORT_UPDATED
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのポートの更新プログラムの拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_UPDATED のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 7FDC963A-92E4-49B2-AB77-FA9C92EEBC25
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_UPDATED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 494258f1a70996145c7023da4b444ca99692dff4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537085"
---
# <a name="oidswitchportupdated"></a>OID\_スイッチ\_ポート\_更新日


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_拡張可能スイッチの拡張機能で拡張可能スイッチ ポートの更新プログラムに関する通知を更新します。 OID は、既に作成されているし、まだ破棄/削除プロセスを開始していないポートにのみ発行されます。 現時点では、のみ、 **PortFriendlyName**フィールドが作成後に更新されるは。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_切り替える\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体は、拡張可能スイッチ ポートを指定します対象の更新の通知が行われました。

拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_スイッチ\_ポート\_更新日。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229) OID 要求に関連付けられている構造体。

-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

**注**  拡張可能スイッチの拡張機能は OID の OID のセット要求を発行する必要があります\_切り替える\_ポート\_更新されました。

 

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のセットの要求が完了すると\_切り替える\_ポート\_更新し、次のステータス コードを返します。

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
[*DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598229)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)

 

 




