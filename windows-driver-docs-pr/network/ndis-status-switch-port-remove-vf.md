---
title: NDIS_STATUS_SWITCH_PORT_REMOVE_VF
description: NDIS_STATUS_SWITCH_PORT_REMOVE_VF 状態の表示は、Hyper-v 拡張可能スイッチ転送拡張機能によって発行され、仮想マシン (VM) ネットワークアダプターと PCI Express (PCIe) 仮想機能 (VF) 間のバインドを削除します。
ms.assetid: D6A52183-C9C6-4F0B-9E25-6C5C16CBEFFE
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_SWITCH_PORT_REMOVE_VF
ms.localizationpriority: medium
ms.openlocfilehash: 548e390ce33177a7cf21484c973bf1d24be194a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843512"
---
# <a name="ndis_status_switch_port_remove_vf"></a>NDIS\_ステータス\_スイッチ\_ポート\_削除\_VF


**NDIS\_状態\_スイッチ\_ポートを\_削除\_** hyper-v 拡張可能スイッチ転送拡張機能によって発行され、仮想マシン (VM) ネットワークアダプターと PCI Express (PCIe) 仮想機能 (vf) 間のバインドが削除されます。 VF は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする、基になる物理ネットワークアダプターによって公開およびサポートされます。

Ndis\_の状態を発行するには **\_\_ポートを変更し\_\_VF**の状態を削除します。そのため、転送拡張機能では、 [**ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)に示されている\_をカプセル化し、nic\_状態\_表示構造をカプセル化し、 [**ndis\_status\_\_nic\_状態**](ndis-status-switch-nic-status.md)状態の表示を発行する必要があります。

このプロセスの詳細については、「 [NDIS\_の状態を発行するためのガイドライン」を参照してください。 **\_\_ポート\_切り替え**て、VF の状態を示す\_を削除](#issuing)します。

<a name="remarks"></a>注釈
-------

PCIe VF は、sr-iov インターフェイスをサポートする基になる物理アダプターによって作成され、割り当てられます。 作成された仮想化スタックは、Hyper-v 子パーティションに VF をアタッチするか、または*割り当て*ます。 このパーティションで実行されるゲストオペレーティングシステムは、基盤となる SR-IOV 物理アダプターの VF にバインドされている仮想マシン (VM) ネットワークアダプターを公開します。

仮想ネットワークアダプターと物理ネットワークアダプターが割り当てられると、VF と VM ネットワークアダプターの間でパケットが直接ルーティングされます。 ただし、拡張可能なスイッチはパケット配信には関係しないため、拡張可能なスイッチポートポリシーはこれらのパケットには適用されません。 これには、アクセス制御リスト (Acl) およびサービスの品質 (QoS) のポートポリシーが含まれます。

拡張可能なスイッチ転送拡張機能では、 **NDIS\_の状態\_スイッチ\_\_ポート**を発行することによって、子パーティションへの vf の割り当てを解除し\_vf 状態の表示を削除することができます。 このように指定すると、VM ネットワークアダプターと、基になる SR-IOV 物理アダプターの VF の間ではなく、拡張可能なスイッチポートを介してパケットが配信されます。 これにより、拡張可能なスイッチポートで受信または送信されたパケットに、拡張可能なスイッチポートポリシーを適用できます。

転送拡張機能によって NDIS の\_状態が\_された場合は、 **\_ポート\_削除\_VF**の状態の表示を削除すると、VM ネットワークアダプターが接続されている拡張可能なスイッチポートが指定されます。

拡張可能なスイッチ転送拡張機能の詳細については、「[拡張機能の転送](https://docs.microsoft.com/windows-hardware/drivers/network/forwarding-extensions)」を参照してください。

### <a href="" id="issuing"></a>NDIS\_状態を発行するためのガイドライン\_スイッチ\_ポート\_削除\_VF ステータス表示

NDIS\_の状態を発行するには **\_\_ポートを切り替え\_、VF**の状態を示す\_を削除します。転送拡張機能は次の手順に従う必要があります。

1.  転送拡張機能は、ndis の **\_ステータス\_スイッチ\_ポート**の NDIS [ **\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造を初期化し、\_VF の表示を削除します。\_ このことを示すために、転送拡張機能は、 **NDIS\_状態\_** 表示構造体の次のメンバーを設定します。

    -   **StatusCode**メンバーを NDIS\_STATUS に設定し、 **\_\_ポート\_切り替えて\_VF を削除**する必要があります。

    -   **Statusbuffer**メンバーは**NULL**に設定する必要があります。

    -   **Statusbuffersize**は0に設定する必要があります。

2.  転送拡張機能は、 [**NDIS\_スイッチ\_NIC\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)表示構造を初期化します。 VF 割り当てを削除するには、転送拡張機能で次のようにメンバーを設定する必要があります。

    -   **DestinationPortId**メンバーは、VM ネットワークアダプターが接続される拡張可能なスイッチポートの識別子に設定する必要があります。

    -   **DestinationNicIndex**メンバーは、指定されたポートに接続されている VM ネットワークアダプターのインデックス値に設定する必要があります。

    -   **SourcePortId**メンバーは、**既定\_ポート\_ID に\_スイッチ\_、NDIS**に設定する必要があります。

    -   **Sourcenicindex**メンバーは、**既定\_\_NIC\_インデックス**に設定する必要があります\_に設定する必要があります。

    -   **Statusindication**メンバーは、NDIS\_ステータスの\_表示構造のアドレスに設定されている必要があります。 [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 、\_の **\_スイッチ\_ポート\_、VF**を示すを削除します。

3.  転送拡張機能によって、ndis [ **\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示されます。 [**ndis\_スイッチ\_NIC\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)表示されます。 このことを示すために、転送拡張機能は、 **NDIS\_状態\_** 表示構造体の次のメンバーを設定します。

    -   **StatusCode**メンバーを[**NDIS\_status\_SWITCH\_NIC\_status**](ndis-status-switch-nic-status.md)に設定する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_スイッチ\_NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体のアドレスに設定する必要があります。

    -   **Statusbuffersize**は、 [**ndis\_スイッチ\_NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体の長さに設定し、ndis\_status\_\_**スイッチ\_ポート**の\_の状態[**を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)に設定する必要があります。\_\_

4.  転送拡張機能は、参照用のモジュールを呼び出して、VM ネットワークアダプターの参照[*カウンターをインクリメント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)する必要があります。 参照/非表示が NDIS\_STATUS\_SUCCESS で完了しない場合、転送拡張*機能は状態*の表示を転送できません。

    **注**  転送拡張機能が OID を受信した場合は、VM アダプターに対して[\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)セット要求[*を呼び出す*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)ことはできません。また、参照ファイルを呼び出して、ステータス表示を転送しないでください。

     

5.  転送拡張機能は、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出して、拡張可能なスイッチドライバースタック内の拡張機能に[**NDIS\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)を転送します。 転送拡張機能は、この関数を呼び出すと、ndis [ **\_ステータス\_スイッチ\_NIC\_状態**](ndis-status-switch-nic-status.md)表示の構造を示すために、[ **ndis\_ステータス\_** 表示構造へのポインターに*statusindication*パラメーターを設定します。

6.  [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)が返された後、転送拡張機能は、VM ネットワークアダプターの参照カウンターを減らすために[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出す必要があります。

転送拡張機能は、転送拡張機能によって削除される各 VF 割り当てについて、前の手順に従う必要がある  に**注意**してください。

 

転送拡張機能がステータス表示を転送する方法の詳細については、「[フィルターモジュールの状態](https://docs.microsoft.com/windows-hardware/drivers/network/filter-module-status-indications)の表示」を参照してください。

### <a name="guidelines-for-determining-vf-assignments"></a>VF の割り当てを決定するためのガイドライン

転送拡張機能は、 [oid\_スイッチ\_NIC\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)の oid クエリ要求を発行することによって、仮想ネットワークアダプターの現在の VF 割り当てを列挙できます。 この要求は、ndis [ **\_スイッチ\_nic\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)構造体を返します。これには、 [**ndis\_スイッチ\_nic\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の配列が含まれています。 各**NDIS\_スイッチ\_NIC\_parameters**構造体は、次のいずれかの環境で公開されているネットワークアダプターのパラメーターを指定します。

-   Hyper-v の親パーティションで実行されている管理オペレーティングシステム。

    このオペレーティングシステムで公開されているネットワークアダプターは、 [**NDIS\_スイッチ\_NIC\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)列挙値**NdisSwitchNicTypeExternal**または**NdisSwitchNicTypeInternal**で指定されます。

-   Hyper-v 子パーティションで実行されるゲストオペレーティングシステム。

    このオペレーティングシステムで公開されているネットワークアダプターは、 [**NDIS\_スイッチ\_NIC\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)列挙値**NdisSwitchNicTypeSynthetic**または**NdisSwitchNicTypeEmulated**で指定されます。

[Oid\_スイッチ\_NIC\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)の oid クエリ要求が、NDIS\_STATUS\_SUCCESS の状態で完了した場合、転送拡張機能は、返された配列内の各[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造を検査することで、VF 割り当てを決定できます。 **Ndis\_スイッチ\_nic\_parameters**構造体の**vfassigned**メンバーが**TRUE**に設定されている場合、 **ndis\_スイッチ\_nic\_PARAMETERS**構造に対応するネットワークアダプターが VF に割り当てられます。

転送拡張機能は、NDIS\_の状態を発行することによって割り当てを削除できます。 **\_スイッチ\_ポート\_削除\_VF**の状態を示します。 この場合、転送拡張機能によって、 [**ndis\_スイッチ\_nic\_\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)の**DestinationPortId**メンバーを設定する必要があります。これは、 [**ndis\_スイッチ\_nic\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**ポート id**メンバーの値に示されます。

Ndis\_の状態を発行する方法の詳細については **\_\_\_ポート**を使用して\_vf[の ](#issuing)状態を削除する」を参照してください。\_\_\_\_\_

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
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_スイッチ\_NIC\_の状態**](ndis-status-switch-nic-status.md)

[**NDIS\_スイッチ\_NIC\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)

[**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NDIS\_スイッチ\_NIC\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)

[OID\_スイッチ\_NIC\_配列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)

 

 




