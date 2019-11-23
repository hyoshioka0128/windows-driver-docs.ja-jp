---
title: OID_SWITCH_NIC_CREATE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セット要求を発行して、拡張可能なスイッチポートとの間に新しい接続が確立されていることを、基になる拡張可能なスイッチ拡張機能に通知 OID_SWITCH_NIC_CREATE します。外部または仮想ネットワークアダプター。 接続が完全に確立されると、拡張可能スイッチのプロトコルエッジは OID_SWITCH_NIC_CONNECT の OID セット要求を発行します。
ms.assetid: 1D6B2C6B-A63E-4A20-B534-AF12714F5FB5
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_NIC_CREATE
ms.localizationpriority: medium
ms.openlocfilehash: 1bbb07902faf3d85eefd456f0cd7c814af03a372
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843959"
---
# <a name="oid_switch_nic_create"></a>OID\_スイッチ\_NIC の作成\_


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_\_NIC を作成して、拡張可能なスイッチポートと外部または仮想ネットワークアダプターとの間に新しい接続が確立されていることを基になる拡張可能なスイッチ拡張機能に通知します。 接続が完全に確立された後、拡張可能スイッチのプロトコルエッジは、oid の OID セット要求を発行し[\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**ポート id**メンバーは、作成通知を行う拡張可能なスイッチポートを指定します。 拡張可能なスイッチ拡張機能では、 [oid\_スイッチ\_ポート\_配列](oid-switch-port-array.md)の oid クエリ要求を発行することによって、拡張可能スイッチ上のこのポートとその他のポートのパラメーター情報を取得できます。

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**インデックス**メンバーは、作成通知を行うネットワークアダプターのインデックスを指定します。 指定された**インデックス**値を持つネットワークアダプターは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されています。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

Oid\_oid セット要求を受信すると\_NIC\_作成されますが、拡張機能は次のガイドラインに従う必要があります。

-   この拡張機能では、OID 要求に関連付けられている[**NIC\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)を変更することはできません。

-   OID\_スイッチ\_NIC\_CREATE 要求では、新しい拡張可能なスイッチ接続が確立されていることと、指定されたポートでパケットトラフィックが間もなく開始される可能性があることが拡張機能に通知されます。 ただし、拡張可能スイッチのプロトコルエッジが oid セット要求を発行するまで、拡張機能はポートを使用できません[\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)します。 この OID が発行されるまでは、拡張機能で次の操作を実行することはできません。

    -   Oid\_スイッチ\_NIC\_CREATE OID 要求が発行された、拡張可能なスイッチポートのネットワークアダプター接続へのパケットトラフィックを生成します。

    -   Oid 要求を転送するか、oid 要求を送信して、基になるネットワークアダプターに[\_nic\_要求を\_](oid-switch-nic-request.md)します。これにより、OID\_スイッチ\_NIC\_CREATE oid 要求が発行されました。

    -   [**Ndis\_status\_スイッチ\_nic\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の発生を転送または開始します。基になるネットワークアダプターでは、OID\_スイッチ\_NIC\_CREATE oid 要求が発行されています。

    -   参照可能なスイッチポートで、指定されたネットワークアダプター接続の拡張可能スイッチ参照カウンターをインクリメントするには、参照/[*上書き*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)を呼び出します。

    拡張機能は、oid の OID 要求\_スイッチ\_NIC\_CREATE および[oid\_スイッチ\_nic\_接続](oid-switch-nic-connect.md)の間で、指定されたポートの送信または受信パケットを**インターセプト  こと**があります。 この場合、拡張機能は、送信または受信パケット要求をキャンセルせずに転送する必要があります。

     

-   拡張機能は、OID 要求に対して\_受け入れられていない\_データ\_NDIS\_状態を返すことによって、作成通知を拒否できます。 たとえば、拡張機能が、指定されたポートで構成されているポリシーを満たすことができない場合、拡張機能は作成通知を拒否する必要があります。

    拡張機能が他の NDIS\_ステータス\_*Xxx*状態コードを返した場合、作成通知も拒否されます。 ただし、NDIS\_STATUS\_リソースを返すなど、一時的なシナリオのステータスコードを返すと、作成通知の再試行が発生する可能性があります。

    拡張機能が OID 要求を拒否しない場合は、要求が完了したときに状態を監視する必要があります。 拡張機能は、拡張可能なスイッチコントロールパスまたは拡張可能なスイッチインターフェイスで、基になる拡張機能によって OID 要求が拒否されたかどうかを判断するために、この処理を実行します。

    この拡張機能では、 [**NDIS\_スイッチ\_NIC\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造の**インデックス**メンバーがネットワークアダプターのインデックス値を0に指定している場合にのみ、OID 要求を拒否  ことに**注意**してください。

     

-   拡張機能が作成通知を拒否しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、この OID 要求を拡張可能なスイッチドライバースタック内の基になる拡張機能に転送する必要があります。

    拡張機能では、この OID 要求の完了状態を監視する必要がある  に**注意**してください。 拡張機能はこれを行い、拡張可能なスイッチドライバースタック内の基になる拡張機能が作成通知を拒否したかどうかを検出します。

     

-   拡張機能が[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出してこの OID 要求を転送する場合、拡張機能は、拡張可能なスイッチポートとの間でパケットトラフィックを即座に受信することはありません。 さらに、拡張機能では、拡張可能なスイッチポートの送信トラフィックや受信トラフィックをすぐに挿入することはできません。

-   拡張可能スイッチのプロトコルエッジが oid セット要求を発行すると、拡張可能なスイッチポートにパケットトラフィックを転送できるようになります。 [\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)します。

    **注**  一部の状況では、OID [\_スイッチ\_\_NIC](oid-switch-nic-connect.md)の oid セット要求が発行される前に、拡張可能スイッチによってポートにパケットトラフィックが転送されることがあります。

     

-   拡張可能スイッチの外部ネットワークアダプターは、1つまたは複数の基になる物理アダプターにバインドできます。 外部ネットワークアダプターにバインドされているすべての物理ネットワークアダプターについて、拡張可能スイッチのプロトコルエッジは、OID\_の別の OID セット要求を発行し\_NIC\_作成します。 各 OID セット要求は、別のネットワークアダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

    拡張機能は、基になる物理アダプターごとに接続状態を維持する必要があります。 物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)」を参照してください。

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

拡張機能では、\_スイッチ\_NIC\_CREATE の独自の OID セット要求を発行してはいけない  に**注意**してください。

 

### <a name="return-status-codes"></a>ステータスコードを返す

拡張機能が oid の OID セット要求を完了すると、\_スイッチ\_NIC の作成\_、次のステータスコードのいずれかが返されます。

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
<td><p>拡張機能は作成通知を拒否します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>リソースの状態が低いため、この拡張機能は作成通知を拒否します。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>この拡張機能は、その他の理由で作成通知を拒否します。</p></td>
</tr>
</tbody>
</table>

 

**注**  は、拡張機能が OID セット要求を完了した場合、NDIS\_STATUS\_SUCCESS を返さないようにする必要があります。

 

拡張機能が oid の OID 設定要求を完了していない場合\_\_NIC の作成\_作成,、要求は、拡張可能なスイッチの基になるミニポートエッジによって完了します。 基になるミニポートエッジは、この OID セット要求に対して次の状態コードを返します。

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

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




