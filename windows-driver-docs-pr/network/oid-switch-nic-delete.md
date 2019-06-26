---
title: OID_SWITCH_NIC_DELETE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのドライバー スタックを OID_SWITCH_NIC_DELETE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 7564EA39-09F5-45A3-81A0-F8DD2B23B639
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bfe9904e4ff964ce46bde43707e45c0ee2814b59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379750"
---
# <a name="oidswitchnicdelete"></a>OID\_スイッチ\_NIC\_削除


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_拡張可能スイッチのドライバー スタックを削除します。 この OID 要求は、拡張可能スイッチ ポートとネットワーク アダプター間の接続の削除に関する拡張可能スイッチの拡張機能を基になるに通知します。 拡張可能スイッチのプロトコル edge 以前に通知の拡張機能の OID セットの要求の発行時にこの接続が削除されているある[OID\_切り替える\_NIC\_切断](oid-switch-nic-disconnect.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造では、ポートを指定の削除通知が行わします。 拡張可能スイッチ拡張機能の OID クエリ要求を発行して拡張可能スイッチには、これと他のポートのパラメーター情報を取得できます[OID\_切り替える\_ポート\_配列](oid-switch-port-array.md)します。

**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体は、ネットワーク アダプターのインデックスを指定します。対象の通知の削除が行われました。 指定したネットワーク アダプター**インデックス**値がで指定された拡張可能スイッチ ポートに接続されている、 **PortId**メンバー。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)します。

プロトコルの前に拡張可能スイッチの端の問題、OID\_切り替える\_NIC\_DELETE 要求を送信保留中のすべてまたは指定したネットワーク アダプターの接続されているは、パケットの要求を受信することを保証完了しました。 プロトコルのエッジには、アダプターの接続の OID 要求の保留中のすべてが完了したらと、アダプターの接続の拡張可能スイッチの参照カウンターがゼロの値を持つことも保証されます。

**注**  場合は、拡張機能は呼び出すことによって、ネットワーク アダプターの拡張可能スイッチ参照カウンターをインクリメントする必要がある[ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)、OID\_スイッチ\_NIC\_参照カウンターが 0 以外の場合は、削除要求は発行されません。 拡張機能をデクリメント拡張可能スイッチの参照カウンターを呼び出した[ *DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)します。

 

拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_スイッチ\_NIC\_を削除します。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) OID 要求に関連付けられている構造体。

-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能は、要求を完了する必要があります。

-   拡張機能は、OID の独自の OID セット要求を発行する必要があります\_スイッチ\_NIC\_を削除します。

-   拡張可能スイッチの外部ネットワーク アダプターは、1 つまたは複数の基になる物理アダプターにバインドできます。 拡張可能スイッチのプロトコルのエッジが OID の独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべての物理ネットワーク アダプターの\_切り替える\_NIC\_を削除します。 各 OID セットの要求では、別のネットワーク アダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)します。

    拡張機能では、基になる各物理アダプターの接続状態を維持する必要があります。 外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)します。

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_を削除し、次のステータス コードを返します。

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
[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_スイッチ\_NIC\_切断](oid-switch-nic-disconnect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




