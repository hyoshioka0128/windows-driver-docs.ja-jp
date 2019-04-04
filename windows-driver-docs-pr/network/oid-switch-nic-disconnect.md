---
title: OID_SWITCH_NIC_DISCONNECT
description: HYPER-V 拡張可能なプロトコル edge スイッチのオブジェクト識別子 (OID) の設定、拡張可能スイッチ ポートとネットワーク アダプター間の接続されている拡張可能スイッチの拡張機能を基になるかを通知する OID_SWITCH_NIC_DISCONNECT の要求の問題破棄されます。 接続は完全に破棄して、後に拡張可能スイッチのプロトコルのエッジは OID_SWITCH_NIC_DELETE の OID セットの要求を発行します。
ms.assetid: 367081A7-F259-4132-B857-C956C0F2829C
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_DISCONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b60e836b625a6b24a145ce1900fac299874b428d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559036"
---
# <a name="oidswitchnicdisconnect"></a>OID\_スイッチ\_NIC\_切断


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_スイッチ\_NIC\_拡張可能スイッチの拡張機能を基になる通知を切断する間の接続、拡張可能スイッチのポートおよびネットワーク アダプターは破棄されているされます。 拡張可能スイッチのプロトコルのエッジがの OID セットの要求を発行後、接続が完全に破棄、 [OID\_切り替える\_NIC\_削除](oid-switch-nic-delete.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体。

<a name="remarks"></a>注釈
-------

**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体は、ネットワーク アダプターのインデックスを指定します。対象の切断の通知が行われました。 指定したネットワーク アダプター**インデックス**値がで指定された拡張可能スイッチ ポートに接続されている、 **PortId**メンバー。 これらのインデックス値の詳細については、[ネットワーク アダプターのインデックス値](https://msdn.microsoft.com/library/windows/hardware/hh598258)を参照してください。

拡張機能は、OID の OID のセット要求を処理する場合これらのガイドラインに従う必要があります\_スイッチ\_NIC\_切断します。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215) OID 要求に関連付けられている構造体。

-   OID\_切り替える\_NIC\_切断要求には、指定したネットワーク アダプターと拡張可能スイッチ ポートの間で拡張可能スイッチ接続が破棄されている拡張機能のみに通知します。 拡張機能はこの OID 要求を処理した後、次いない行う必要があります。

    -   拡張可能スイッチ ポートでのネットワーク アダプターの接続にパケット トラフィックを生成、OID\_切り替える\_NIC\_OID の切断要求が発行します。

    -   呼び出す[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)拡張可能スイッチ ポートで指定されたネットワーク アダプター接続の拡張可能スイッチの参照カウンターをインクリメントします。

    -   転送するかの OID 要求を発信[OID\_スイッチ\_NIC\_要求](oid-switch-nic-request.md)を基になるネットワーク アダプターに OID\_スイッチ\_NIC\_切断 OID 要求が発行されました。

        **注**、拡張機能が呼び出された場合[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294) OID の前に拡張可能スイッチの参照カウンターをインクリメントする\_切り替える\_NIC\_切断が発行された、拡張機能の転送や OID 要求を発信できますも。



    -   転送するか元の状態インジケーターの NDIS [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)を基になるネットワーク アダプターからOID\_スイッチ\_NIC\_OID の切断要求が発行されています。

        **注**、拡張機能が呼び出された場合[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294) OID の前に拡張可能スイッチの参照カウンターをインクリメントする\_切り替える\_NIC\_切断が発行された、拡張機能の転送や NDIS 状態インジケーターを発信できますも。

        **注**、拡張機能が以前に呼び出された場合[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)拡張可能スイッチの参照カウンターをインクリメントする必要はありません発信元または転送するには、その呼び出しを同期するにはOID 要求または拡張可能な HYPER-V を管理するそのコードと状態インジケーターの NDIS OID 要求を切り替えます。 拡張機能が参照カウンターをインクリメント後、拡張可能スイッチのインターフェイスの OID セットの要求を発行しません[OID\_切り替える\_NIC\_削除](oid-switch-nic-delete.md)します。

-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能は、要求を完了する必要があります。

-   拡張可能スイッチの外部ネットワーク アダプターは、1 つまたは複数の基になる物理アダプターにバインドできます。 拡張可能スイッチのプロトコルのエッジが OID の独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべての物理ネットワーク アダプターの\_切り替える\_NIC\_切断します。 各 OID セットの要求では、別のネットワーク アダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、[ネットワーク アダプターのインデックス値](https://msdn.microsoft.com/library/windows/hardware/hh598258)を参照してください。

    拡張機能では、基になる各物理アダプターの接続状態を維持する必要があります。 外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、[型の物理ネットワーク アダプターの構成](https://msdn.microsoft.com/library/windows/hardware/hh582274)を参照してください。

**注**、拡張機能は、OID の独自の OID セット要求を発行する必要があります\_スイッチ\_NIC\_切断します。

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、[Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_切断し、次のステータス コードを返します。

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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)