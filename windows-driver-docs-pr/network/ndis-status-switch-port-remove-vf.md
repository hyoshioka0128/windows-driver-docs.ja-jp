---
title: NDIS_STATUS_SWITCH_PORT_REMOVE_VF
description: NDIS_STATUS_SWITCH_PORT_REMOVE_VF 状態の表示は、転送拡張機能を仮想マシン (VM) ネットワーク アダプターと PCI Express (PCIe) 仮想機能 (VF) 間のバインドを削除する HYPER-V 拡張可能スイッチによって発行されます。
ms.assetid: D6A52183-C9C6-4F0B-9E25-6C5C16CBEFFE
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_SWITCH_PORT_REMOVE_VF ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d54d3304f3ba0bddb7a46a70d70a36a2b181fc88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353369"
---
# <a name="ndisstatusswitchportremovevf"></a>NDIS\_状態\_スイッチ\_ポート\_削除\_VF


**NDIS\_状態\_切り替える\_ポート\_削除\_VF**状態を示す値が転送のバインドを削除する拡張機能、HYPER-V 拡張可能スイッチによって発行されました。仮想マシン (VM) ネットワーク アダプターと PCI Express (PCIe) 仮想機能 (VF) の間 VF が公開され、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする、基になる物理ネットワーク アダプターによってサポートされています。

発行するには、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態を示す値、転送拡張機能は、で示す値をカプセル化する必要があります[**NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造と問題を[ **NDIS\_ステータス\_スイッチ\_NIC\_状態**](ndis-status-switch-nic-status.md)状態を示す値。

このプロセスの詳細については、次を参照してください[発行するためのガイドライン、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態表示。](#issuing).

<a name="remarks"></a>注釈
-------

PCIe VF が作成され、SR-IOV 対応インターフェイスをサポートする、基になる物理アダプターが割り当てられます。 作成されると、仮想化スタックがアタッチ、または*割り当てます*、VF HYPER-V 子パーティションにします。 このパーティションで実行されているゲスト オペレーティング システムでは、基になる、SR-IOV 対応の物理アダプターの VF にバインドされている仮想マシン (VM) ネットワーク アダプターを公開します。

アダプターが割り当てられている仮想および物理ネットワーク後、は、パケットは VF と VM ネットワーク アダプター間で直接ルーティングされます。 ただし、拡張可能スイッチ パケット配信に関係のない、ために、これらのパケットには拡張可能スイッチ ポートのポリシーは適用されません。 これにより、ポートへのアクセス ポリシーが含まれます。 リスト (Acl) とサービスの品質 (QoS) を制御します。

転送拡張機能を拡張可能スイッチは、子パーティションに VF の割り当てを削除するを発行して、 **NDIS\_状態\_切り替える\_ポート\_削除\_VF**状態を示す値。 この通知は、パケットの VM ネットワーク アダプターと基になる、SR-IOV 対応の物理アダプターの VF 間で直接の代わりに、拡張可能スイッチ ポート経由で配信されるとします。 これにより、拡張可能スイッチ ポートの受信または拡張可能スイッチ ポート経由で送信されるパケットに適用するポリシー。

転送拡張機能は、ときに、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態の表示を拡張可能スイッチのポートを指定しますVM のネットワーク アダプターが接続されています。

拡張可能スイッチの転送拡張機能の詳細については、次を参照してください。[転送拡張機能](https://msdn.microsoft.com/library/windows/hardware/hh598148)します。

### <a href="" id="issuing"></a>NDIS を発行するためのガイドライン\_状態\_スイッチ\_ポート\_削除\_VF 状態表示

発行するには、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態を示す値、転送拡張機能が次の手順に従う必要があります。

1.  転送拡張機能を初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)用の構造、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**を示す値。 この表示では、転送拡張機能設定の次のメンバー、 **NDIS\_状態\_INDICATION**構造。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_スイッチ\_ポート\_削除\_VF**します。

    -   **StatusBuffer**にメンバーを設定する必要があります**NULL**します。

    -   **StatusBufferSize**を 0 に設定する必要があります。

2.  転送拡張機能を初期化します、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造体。 VF の割り当てを削除するには転送拡張機能は、次のように、メンバーを設定する必要があります。

    -   **DestinationPortId**メンバーは、VM のネットワーク アダプターが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。

    -   **DestinationNicIndex**メンバーは、指定したポートに接続されている VM ネットワーク アダプターのインデックス値に設定する必要があります。

    -   **SourcePortId**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_ポート\_ID**します。

    -   **SourceNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

    -   **StatusIndication**メンバーのアドレスに設定する必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)用の構造、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**を示す値。

3.  転送拡張機能を初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)用の構造、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)を示す値。 この表示では、転送拡張機能設定の次のメンバー、 **NDIS\_状態\_INDICATION**構造。

    -   **StatusCode**にメンバーを設定する必要があります[ **NDIS\_状態\_スイッチ\_NIC\_状態**](ndis-status-switch-nic-status.md)します。

    -   **StatusBuffer**メンバーのアドレスに設定する必要があります、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造体。

    -   **StatusBufferSize**の長さ (バイト単位) を設定する必要があります、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造と[ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)用の構造、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**を示す値。

4.  転送拡張機能を呼び出す必要があります[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)を VM のネットワーク アダプターの参照カウンターをインクリメントします。 場合*ReferenceSwitchNic* NDIS が完了しなかった\_状態\_成功すると、転送拡張機能は、状態を示す値を転送する必要があります。

    **注**  転送拡張機能が受信した場合、 [OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)設定呼び出さないでください VM アダプターの要求[。*ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)も、状態を示す値を転送します。

     

5.  転送拡張機能を呼び出す[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)転送するように、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)拡張可能スイッチのドライバー スタックの拡張機能に関連します。 転送拡張機能は、この関数を呼び出しとき、に、設定、 *StatusIndication*パラメーターへのポインターを**NDIS\_状態\_INDICATION** の構造[**NDIS\_状態\_スイッチ\_NIC\_状態**](ndis-status-switch-nic-status.md)を示す値。

6.  後[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)返します、転送拡張機能を呼び出す必要があります[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)を下げるには、VM のネットワーク アダプターの参照カウンターです。

**注**  転送拡張機能が、転送拡張機能を削除する VF 割り当てごとに、前の手順に従う必要があります。

 

転送拡張機能で状態インジケーターを転送する方法の詳細については、次を参照してください。[フィルター モジュールの状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/ff550020)します。

### <a name="guidelines-for-determining-vf-assignments"></a>VF の割り当てを決定するためのガイドライン

転送拡張機能の OID クエリ要求を発行して仮想ネットワーク アダプターの現在の VF 割り当てを列挙できる[OID\_スイッチ\_NIC\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598261)します。 この要求を返します、 [ **NDIS\_スイッチ\_NIC\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598212)構造体の配列を含む[ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体。 各**NDIS\_スイッチ\_NIC\_パラメーター**構造体は、次の環境のいずれかで公開されているネットワーク アダプターのパラメーターを指定します。

-   HYPER-V 親パーティションで実行されている管理オペレーティング システム。

    このオペレーティング システムで公開されているネットワーク アダプターがで指定された、 [ **NDIS\_スイッチ\_NIC\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598218)列挙値の**NdisSwitchNicTypeExternal**または**NdisSwitchNicTypeInternal**します。

-   HYPER-V 子パーティションで実行されているゲスト オペレーティング システム。

    このオペレーティング システムで公開されているネットワーク アダプターがで指定された、 [ **NDIS\_スイッチ\_NIC\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598218)列挙値の**NdisSwitchNicTypeSynthetic**または**NdisSwitchNicTypeEmulated**します。

OID のクエリの要求の場合は[OID\_スイッチ\_NIC\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598261)NDIS の状態になって完了\_状態\_成功すると、転送拡張機能は VF を判断できます各を調べることによって割り当て[ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)返された配列の構造体。 場合、 **VFAssigned**のメンバー、 **NDIS\_スイッチ\_NIC\_パラメーター**構造に設定されている**TRUE**、ネットワーク アダプター対応する、 **NDIS\_スイッチ\_NIC\_パラメーター**構造体は、VF に割り当てられます。

転送拡張機能は発行することによって、割り当てを削除することができます、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態を示す値。 この場合、転送拡張機能を設定する必要があります、 **DestinationPortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_状態\_を示す値** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)の値に、 **PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh598215)構造体。

発行する方法について、 **NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態を示す値を参照してください[発行するためのガイドライン、**NDIS\_状態\_スイッチ\_ポート\_削除\_VF**状態表示](#issuing)します。

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
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_スイッチ\_NIC\_状態**](ndis-status-switch-nic-status.md)

[**NDIS\_スイッチ\_NIC\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598212)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[**NDIS\_スイッチ\_NIC\_型**](https://msdn.microsoft.com/library/windows/hardware/hh598218)

[OID\_スイッチ\_NIC\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598261)

 

 




