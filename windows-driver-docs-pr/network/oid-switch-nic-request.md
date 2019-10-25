---
title: OID_SWITCH_NIC_REQUEST
description: OID_SWITCH_NIC_REQUEST のオブジェクト識別子 (OID) メソッド要求は、OID 要求をカプセル化して Hyper-v 拡張可能スイッチの外部ネットワークアダプターに転送するために使用されます。
ms.assetid: 7EF4D950-D18E-400A-B1DD-39768A16E4C4
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_NIC_REQUEST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3a4e2de06a823bc94372b10e3eac3dd7716b8c69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843953"
---
# <a name="oid_switch_nic_request"></a>OID\_スイッチ\_NIC\_要求


Oid\_スイッチ\_NIC\_要求のオブジェクト識別子 (OID) メソッド要求は、OID 要求をカプセル化して Hyper-v 拡張可能スイッチの外部ネットワークアダプターに転送するために使用されます。 これにより、外部ネットワークアダプターにバインドされている、基になる物理ネットワークアダプターのドライバーに、カプセル化された OID 要求を配信できます。

この OID 要求は、拡張可能なスイッチポートに接続されている他のネットワークアダプターに対して発行された OID 要求をカプセル化するためにも使用されます。 この場合は、拡張機能による検査のために、カプセル化された OID 要求が拡張可能なスイッチドライバースタックを介して転送されます。

[**Ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)へのポインターが含まれています。これには、NIC\_OID\_の要求構造が含まれます。 この構造体は、OID 要求の転送情報を指定します。 この構造体には、転送される OID 要求の元の**NDIS\_oid\_要求**構造へのポインターも含まれます。

<a name="remarks"></a>注釈
-------

OID 要求が Hyper-v 拡張可能スイッチインターフェイスに到着すると、拡張可能なスイッチ制御パスに転送されるようにカプセル化されます。 これらの OID 要求には、次のものが含まれます。

-   インターネットプロトコルセキュリティ (IPsec)、バーチャルマシンキュー (VMQ)、シングルルート i/o 仮想化 (SR-IOV) の要求など、ハードウェアオフロードの OID 要求。 これらの OID 要求は、Hyper-v の親パーティションの管理オペレーティングシステムで実行されるプロトコルまたはフィルタードライバーによって発行されます。

    これらの OID 要求が拡張可能スイッチインターフェイスに到着すると、拡張可能スイッチのプロトコルエッジは、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造内に oid 要求をカプセル化します。 プロトコルエッジは、この構造体のメンバーを次のように設定します。

    -   **DestinationPortId**メンバーと**DestinationNicIndex**メンバーは、外部ネットワークアダプターの対応する値に設定されます。

    -   OID 要求が Hyper-v 子パーティションから送信された場合、 **SourcePortId**および**Sourcenicindex**メンバーは、パーティションによって使用されるポートおよびネットワークアダプターの対応する値に設定されます。 それ以外の場合、 **SourcePortId**および**Sourcenicindex**のメンバーは0に設定されます。

        **メモ** 拡張機能は、OID 要求を転送またはリダイレクトする場合に、これらのメンバーの値を保持する必要があります。



    -   **OidRequest**メンバーは、カプセル化された oid 要求の[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造へのポインターに設定されます。

    次に、プロトコルエッジは OID\_スイッチ\_NIC\_要求を発行して、カプセル化された OID 要求を外部ネットワークアダプターへの拡張可能なスイッチ制御パスに転送します。

    基になる転送拡張機能は、外部ネットワークアダプターにバインドされている物理ネットワークアダプターに、カプセル化されたハードウェアオフロード OID 要求をリダイレクトすることができます。 たとえば、拡張機能が、外部ネットワークアダプターにバインドされている拡張可能なスイッチチームからの物理ネットワークアダプターをサポートしている場合、OID\_スイッチ\_NIC\_要求要求を負荷の物理アダプターに転送できます。ハードウェアオフロードをサポートする分散フェールオーバー (LBFO) チーム。 この手順の詳細については、「[物理ネットワークアダプターに対するハードウェアオフロード OID 要求の管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-hardware-offload-oid-requests-to-physical-network-adapters)」を参照してください。

    拡張可能なスイッチチームの詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

-   [Oid\_802\_3\_\_のマルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)と oid を含むマルチキャスト oid 要求\_\_[802\_3\_削除\_マルチキャストアドレス](oid-802-3-delete-multicast-address.md)。 これらの OID 要求は、プロトコルとフィルタードライバーによって発行され、管理オペレーティングシステムまたは Hyper-v 子パーティションのゲストオペレーティングシステムのいずれかで実行されます。

    これらの OID 要求が拡張可能スイッチインターフェイスに到着すると、拡張可能スイッチのプロトコルエッジは、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造内に oid 要求をカプセル化します。 また、プロトコルエッジは、 **SourcePortId**および**Sourcenicindex**メンバーを、OID 要求の発生元のポートおよびネットワークアダプターの対応する値に設定します。 次に、プロトコルエッジは OID\_スイッチ\_NIC\_要求を発行して、カプセル化された OID 要求を、基になる拡張機能によって検査する拡張可能なスイッチコントロールパスに転送します。

    **メモ** この場合、プロトコルエッジは**DestinationPortId**メンバーと**DestinationNicIndex**メンバーをゼロに設定します。 これは、カプセル化された OID 要求が、コントロールパス内の拡張機能に配信されることを指定します。

    基になる転送拡張機能は、カプセル化されたこれらの OID 要求を検査し、指定したマルチキャストアドレス情報を保持できます。 たとえば、拡張可能なスイッチポートに転送するマルチキャストパケットが発生した場合、この情報が必要になることがあります。

    詳細については、「 [Hyper-v 子パーティションからの OID 要求の転送](https://docs.microsoft.com/windows-hardware/drivers/network/forwarding-oid-requests-from-a-hyper-v-child-partition)」を参照してください。

また、転送拡張機能は、カプセル化された OID 要求を外部ネットワークアダプターにバインドされている物理ネットワークアダプターに転送するために、OID\_スイッチ\_NIC\_要求を発行することもできます。 これにより、拡張機能が独自の OID 要求を発信したり、既存の OID 要求を外部ネットワークアダプターにバインドされている物理ネットワークアダプターにリダイレクトしたりすることができます。 このためには、次の手順に従って拡張機能を実行する必要があります。

1.  この拡張機能は、参照元の物理ネットワークアダプターのインデックスの参照[*カウンターをインクリメントするため*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)に参照を参照します。 これにより、拡張可能なスイッチインターフェイスでは、参照カウンターが0以外の場合に、物理ネットワークアダプターの接続が削除されません。

    **メモ** 拡張可能スイッチインターフェイスは、参照カウンターが0以外の場合に、物理ネットワークアダプター接続を切断できます。 詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

2.  この拡張機能は、次の方法で[**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造を初期化することによって、oid 要求をカプセル化します。

    -   **DestinationPortId**メンバーは、外部ネットワークアダプターが接続される拡張可能なスイッチポートの識別子に設定する必要があります。
    -   **DestinationNicIndex**メンバーには、基になる物理ネットワークアダプターの0以外のインデックス値を設定する必要があります。
    -   拡張機能が Hyper-v 子パーティションの代わりに生成される場合、 **SourcePortId**および**Sourcenicindex**メンバーは、パーティションで使用されるポートおよびネットワークアダプターの対応する値に設定されます。 それ以外の場合、 **SourcePortId**および**Sourcenicindex**のメンバーは0に設定されます。

        たとえば、拡張機能が子パーティションのハードウェアオフロードリソースを管理している場合、 **SourcePortId**および**Sourcenicindex**メンバーを設定して、カプセル化されたハードウェアオフロード OID 要求のパーティションを指定する必要があります。

    -   **OidRequest**メンバーは、カプセル化された oid 要求の初期化済みの[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造へのポインターに設定する必要があります。

3.  この拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、指定された宛先拡張可能スイッチポートとネットワークアダプターに OID 要求を転送します。

4.  NDIS が[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)関数を呼び出すと、拡張機能は[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出して、宛先の物理ネットワークアダプターのインデックスの参照カウンターをクリアします。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_NIC\_要求の OID クエリ要求を完了し、次のステータスコードのいずれかを返します。

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
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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
[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)