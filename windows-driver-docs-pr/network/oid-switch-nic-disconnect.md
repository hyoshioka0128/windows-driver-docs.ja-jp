---
title: OID_SWITCH_NIC_DISCONNECT
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、OID_SWITCH_NIC_DISCONNECT のオブジェクト識別子 (OID) セット要求を発行し、拡張可能なスイッチポートとネットワークアダプター間の接続があることを、基になる拡張可能なスイッチ拡張機能に通知します。破損しています。 接続が完全に切断された後、拡張可能スイッチのプロトコルエッジは OID_SWITCH_NIC_DELETE の OID セット要求を発行します。
ms.assetid: 367081A7-F259-4132-B857-C956C0F2829C
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_NIC_DISCONNECT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d665c102aa66c98d2b02836d458d48baf5dcfe4c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843955"
---
# <a name="oid_switch_nic_disconnect"></a>OID\_スイッチ\_NIC\_切断


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの OID の要求を発行し\_スイッチ\_NIC\_切断し、拡張可能なスイッチポートとの間の接続を持つ、基になる拡張可能なスイッチ拡張機能に通知します。ネットワークアダプターが破損しています。 接続が完全に切断された後、拡張可能スイッチのプロトコルエッジは、oid の oid セット要求を発行して[\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**インデックス**メンバーは、切断通知を行うネットワークアダプターのインデックスを指定します。 指定された**インデックス**値を持つネットワークアダプターは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されています。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

拡張機能は、OID の OID セット要求を処理するときに、次のガイドラインに従う必要があります\_スイッチ\_NIC\_切断:

-   この拡張機能では、OID 要求に関連付けられている[**NIC\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)を変更することはできません。

-   OID\_スイッチ\_NIC\_切断要求では、指定されたネットワークアダプターと拡張可能なスイッチポートの間で拡張スイッチ接続が切断されていることが拡張機能に対してのみ通知されます。 拡張機能がこの OID 要求を処理した後、次の操作を行うことはできません。

    -   Oid\_スイッチ\_NIC\_切断 OID 要求が発行された、拡張可能なスイッチポートのネットワークアダプター接続へのパケットトラフィックを生成します。

    -   参照可能なスイッチポートで、指定されたネットワークアダプター接続の拡張可能スイッチ参照カウンターをインクリメントするには、参照/[*上書き*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)を呼び出します。

    -   Oid 要求を転送するか、oid 要求を送信して、基になるネットワークアダプターに[\_nic\_要求を\_](oid-switch-nic-request.md)します。これにより、OID\_スイッチ\_NIC\_切断 oid 要求が発行されます。

        **メモ** OID\_スイッチ\_NIC\_切断が発行される前に、拡張機能が参照可能なスイッチの参照カウンターをインクリメントするように拡張機能[*を呼び出した*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)場合、拡張機能は引き続き oid 要求を転送または開始できます。



    -   [**Ndis\_status\_スイッチ\_nic\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の ndis ステータスの兆候を転送または開始する、基になるネットワークアダプターで、OID\_スイッチ\_NIC\_切断 oid 要求が発行されました。

        **メモ** OID\_スイッチ\_NIC\_切断が発行される前に、拡張機能によって拡張可能なスイッチ参照カウンターがインクリメント[*された*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)場合、拡張機能は依然として NDIS ステータスの兆候を転送または開始できます。

        **メモ** 拡張可能なスイッチ参照[*カウンターをインクリメントするため*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)に既に参照を参照している拡張機能では、その呼び出しを同期して、OID 要求または NDIS ステータスの兆候を hyper-v を管理するコードと共に転送する必要はありません。拡張スイッチ OID 要求。 拡張機能によって参照カウンターがインクリメントされた後は、拡張可能なスイッチインターフェイスは oid\_スイッチの oid セット要求を発行しません[\_NIC\_削除](oid-switch-nic-delete.md)します。

-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を完了できません。

-   拡張可能スイッチの外部ネットワークアダプターは、1つまたは複数の基になる物理アダプターにバインドできます。 外部ネットワークアダプターにバインドされているすべての物理ネットワークアダプターについて、拡張可能スイッチのプロトコルエッジは、OID の個別の OID セット要求を発行し\_スイッチ\_NIC\_切断します。 各 OID セット要求は、別のネットワークアダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

    拡張機能は、基になる物理アダプターごとに接続状態を維持する必要があります。 物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

**メモ** 拡張機能は、\_NIC\_切断を\_スイッチの独自の OID セット要求を発行しないようにする必要があります。

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチの OID クエリ要求を完了し\_NIC\_切断し、次のステータスコードを返します。

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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)