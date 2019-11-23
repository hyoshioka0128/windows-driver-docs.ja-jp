---
title: OID_SWITCH_NIC_DELETE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、OID_SWITCH_NIC_DELETE のオブジェクト識別子 (OID) セット要求を拡張可能なスイッチドライバースタックに発行します。
ms.assetid: 7564EA39-09F5-45A3-81A0-F8DD2B23B639
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_NIC_DELETE
ms.localizationpriority: medium
ms.openlocfilehash: b192b27fecb423aa450be4de6323f082fc517f6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843958"
---
# <a name="oid_switch_nic_delete"></a>OID\_スイッチ\_NIC\_削除


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) set 要求の OID\_スイッチ\_NIC が拡張可能なスイッチドライバースタックに\_削除されます。 この OID 要求は、拡張可能なスイッチポートとネットワークアダプター間の接続の削除について、基になる拡張可能なスイッチ拡張機能に通知します。 拡張スイッチのプロトコルエッジは、oid セット要求を発行したときに、この接続が削除されていることを通知する拡張機能の[\_スイッチ\_NIC\_切断](oid-switch-nic-disconnect.md)します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**ポート id**メンバーは、削除通知を行うポートを指定します。 拡張可能なスイッチ拡張機能では、 [oid\_スイッチ\_ポート\_配列](oid-switch-port-array.md)の oid クエリ要求を発行することによって、拡張可能スイッチ上のこのポートとその他のポートのパラメーター情報を取得できます。

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**インデックス**メンバーは、削除通知が行われるネットワークアダプターのインデックスを指定します。 指定された**インデックス**値を持つネットワークアダプターは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されています。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

拡張可能スイッチのプロトコルエッジが OID\_スイッチ\_NIC\_DELETE 要求を発行する前に、指定されたネットワークアダプター接続に対するすべての保留中の送信または受信パケット要求が完了したことを保証します。 また、プロトコルエッジは、アダプター接続に対するすべての保留中の OID 要求が完了していること、およびアダプター接続の拡張可能なスイッチ参照カウンターの値が0であることも保証します。

**注**  拡張機能によって参照用のスイッチ参照カウンターがネットワークアダプターに対してインクリメントされている場合[*は、参照*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)カウンターが0以外の場合、OID\_スイッチ\_NIC\_DELETE 要求は発行されません。 拡張機能は、 [*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出すことによって拡張可能なスイッチ参照カウンターをデクリメントします。

 

この拡張機能は、次のガイドラインに従って、OID の OID セット要求を処理する必要があります\_スイッチ\_NIC\_削除します。

-   この拡張機能では、OID 要求に関連付けられている[**NIC\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)を変更することはできません。

-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を完了できません。

-   拡張機能では、OID\_スイッチ\_NIC\_削除の独自の OID セット要求を発行することはできません。

-   拡張可能スイッチの外部ネットワークアダプターは、1つまたは複数の基になる物理アダプターにバインドできます。 外部ネットワークアダプターにバインドされているすべての物理ネットワークアダプターについて、拡張可能スイッチのプロトコルエッジは、OID の個別の OID セット要求を発行\_、\_NIC\_削除します。 各 OID セット要求は、別のネットワークアダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

    拡張機能は、基になる物理アダプターごとに接続状態を維持する必要があります。 物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_NIC の OID クエリ要求を完了し\_削除して、次のステータスコードを返します。

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
[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_スイッチ\_NIC\_切断](oid-switch-nic-disconnect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/Nic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




