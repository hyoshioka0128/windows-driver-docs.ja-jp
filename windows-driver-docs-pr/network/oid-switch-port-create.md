---
title: OID_SWITCH_PORT_CREATE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのポートの作成に関する拡張可能スイッチの拡張機能を通知する OID_SWITCH_PORT_CREATE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 579D51CD-0594-4A06-998E-3886E7325D97
ms.date: 08/08/2017
keywords: -OID_SWITCH_PORT_CREATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b785498f3c487260514f9d82f025d203f9cae1cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574047"
---
# <a name="oidswitchportcreate"></a>OID\_スイッチ\_ポート\_を作成します。


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_ポート\_拡張可能スイッチの拡張機能で拡張可能スイッチ ポートの作成についての通知を作成します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体。

<a name="remarks"></a>コメント
-------

**PortId**のメンバー、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229)構造体は、対象のポートを指定します、作成の通知が行わします。

拡張可能スイッチ拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_切り替える\_ポート\_作成。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229) OID 要求に関連付けられている構造体。

-   拡張機能は、NDIS を返すことによって作成の通知を拒否できます\_状態\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、その構成済みポリシー、ポートを強制するリソースを割り当てることができません、ドライバーは作成の通知を拒否する必要があります。

    拡張機能は、その他の NDIS を返す場合\_状態\_*Xxx*エラー ステータス コードを作成の通知が拒否されることもできます。 ただし、NDIS を返すなどの一時的なシナリオに関する状態コードを返す\_状態\_リソースが作成の通知の再試行になる可能性があります。

    場合は、拡張機能が、OID 要求を拒否しては、要求が完了したときに、状態を監視する必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

    ポートのポリシーの詳細については、次を参照してください。[管理の Hyper-v 拡張可能なスイッチのポリシー](https://msdn.microsoft.com/library/windows/hardware/hh598195)します。

-   拡張機能を呼び出す場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)この OID セット要求を転送するように、拡張機能がこの OID 要求の完了状態を監視する必要があります。 拡張機能は、拡張可能スイッチ ドライバー スタック内の基になる拡張機能があるポートの作成の通知を拒否したかどうかを検出するためにします。

-   など、ポートの Oid 要求を発行できる、拡張機能に OID 要求が転送されが正常に完了すると、 [OID\_スイッチ\_ポート\_プロパティ\_ENUM](oid-switch-port-property-enum.md)、まで、OID 要求[OID\_スイッチ\_ポート\_破棄](oid-switch-port-teardown.md)が発行されます。 この OID 要求は、ポートが拡張可能スイッチから削除プロセスを開始する、拡張機能を通知します。

-   拡張機能で指定されたポートにパケットを転送できません、 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598229) OIDの要求が設定されるまで構造体[OID\_スイッチ\_NIC\_CONNECT](oid-switch-nic-connect.md)が発行されが正常に完了します。

**注**  拡張機能は OID の OID のセット要求を発行する必要があります\_スイッチ\_ポート\_作成します。

 

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張機能の OID OID セットの要求が完了すると\_スイッチ\_ポート\_作成で、1 つを返しますの次のステータス コード。

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
<td><p>拡張機能は、作成の通知を拒否しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>拡張機能は、リソース不足状態が原因で、作成通知を拒否しました。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>拡張機能は、他の理由から、作成の通知を拒否しました。</p></td>
</tr>
</tbody>
</table>

 

**注**  NDIS を返す必要がない場合は、拡張機能には、OID セットの要求が完了すると、\_状態\_成功します。

 

拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_ポート\_拡張可能スイッチの基になるミニポート端で作成、要求が完了します。 基になるミニポート edge では、この OID セットの要求の次のステータス コードを返します。

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

 

<a name="requirements"></a>必要条件
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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598229)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[OID\_スイッチ\_ポート\_プロパティ\_列挙型](oid-switch-port-property-enum.md)

 

 




