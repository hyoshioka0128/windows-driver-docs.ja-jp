---
title: OID_SWITCH_NIC_CONNECT
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セット要求を発行して、拡張可能なスイッチポートとネットワークアダプター間のネットワーク接続があることを、基になる拡張可能なスイッチ拡張に通知 OID_SWITCH_NIC_CONNECT ます。完全に確立されました。 プロトコルエッジは、OID_SWITCH_NIC_CREATE の OID セット要求を発行したときに、この接続が確立されていることを、拡張機能に通知しました。
ms.assetid: 98A4AD28-2716-40DD-AE46-70969A23FAB7
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_NIC_CONNECT
ms.localizationpriority: medium
ms.openlocfilehash: fda275d602e5de033400735e8079c9c8d9692002
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843962"
---
# <a name="oid_switch_nic_connect"></a>OID\_スイッチ\_NIC\_接続


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) set 要求 OID\_スイッチ\_NIC\_接続を介して、拡張可能なスイッチポートとネットワークアダプター間のネットワーク接続が完全に確立されていることを基になる拡張可能なスイッチ拡張機能に通知します。 プロトコルエッジには、oid セット要求を発行したときに、この接続が確立されていることを通知する拡張機能があります。 [\_スイッチ\_NIC\_作成](oid-switch-nic-create.md)します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**ポート id**メンバーは、接続通知を行う拡張可能なスイッチポートを指定します。 拡張可能なスイッチ拡張機能は、次の方法で、このポートとその他の拡張可能なスイッチポートのパラメーター情報を取得できます。

-   Oid の OID クエリ要求を発行することによって[\_\_ポート\_配列に切り替え](oid-switch-port-array.md)ます。 拡張機能は、OID\_スイッチ\_パラメーターが、 **IsActive**が TRUE に設定された[**NDIS\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)構造を返す場合にのみ、この oid を[*filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)に発行します。 **IsActive**が FALSE の場合は、拡張機能のミニポートアダプターによって**NETEVENTSWITCHACTIVATE** [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)が発行されるときに、拡張機能によって OID が発行されます。

-   Oid のさまざまな OID セット要求を検査することによって[\_\_ポート\_作成](oid-switch-port-create.md)および[oid\_スイッチ\_ポート\_削除](oid-switch-port-delete.md)します。

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**インデックス**メンバーは、接続通知を行うネットワークアダプターのインデックスを指定します。 指定された**インデックス**値を持つネットワークアダプターは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されています。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

Oid の OID セット要求を受信すると\_スイッチ\_NIC\_接続するために、拡張機能は次のガイドラインに従う必要があります。

-   OID\_スイッチ\_NIC\_接続要求が NDIS\_STATUS\_SUCCESS で完了すると、ネットワーク接続と拡張可能なスイッチポートは完全に動作します。 拡張機能は、ポートのネットワーク接続にパケットトラフィックを生成または転送できます。 拡張機能は、ポートをソースポートとして使用する拡張可能なスイッチ Oid または状態の兆候を発行することもできます。 また、この拡張機能では、参照の参照可能[*Chport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)を呼び出して、ポートの拡張可能なスイッチ参照カウンターを増やすこともできます。

-   この拡張機能では、OID 要求に関連付けられている[**NIC\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)を変更することはできません。

-   拡張機能は、この OID 要求を基になる拡張機能に転送するために、常に[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 拡張機能は OID 要求自体を完了することはできません。

-   拡張可能スイッチの外部ネットワークアダプターは、1つまたは複数の基になる物理アダプターにバインドできます。 外部ネットワークアダプターにバインドされているすべての物理ネットワークアダプターについて、拡張可能スイッチのプロトコルエッジは、OID の別の OID セット要求を発行し\_スイッチ\_NIC\_接続します。 各 OID セット要求は、別のネットワークアダプター接続のインデックス値を指定します。 これらの値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

    拡張機能は、外部ネットワークアダプターにバインドされている、基になる物理アダプターごとに接続状態を維持する必要があります。 物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

拡張機能は、\_スイッチ\_NIC\_CONNECT の独自の OID セット要求を発行してはいけない  に**注意**してください。

 

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_\_NIC の設定要求を完了し、次の状態コードを返します。

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
[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC の作成\_](oid-switch-nic-create.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




