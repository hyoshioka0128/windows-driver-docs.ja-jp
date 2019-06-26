---
title: OID_SWITCH_NIC_CREATE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジに拡張可能スイッチ拡張機能を基になる、拡張可能スイッチ ポートの間に新しい接続が確立されることを通知する要求 OID_SWITCH_NIC_CREATE のセット オブジェクト識別子 (OID) を発行して、外部接続または仮想ネットワーク アダプター。 接続が完全に確立されると、拡張可能スイッチのプロトコルのエッジは OID_SWITCH_NIC_CONNECT の OID セットの要求を発行します。
ms.assetid: 1D6B2C6B-A63E-4A20-B534-AF12714F5FB5
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_CREATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8ecd9cc44258f7f2f94942fe7b7982fecc2c14c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379751"
---
# <a name="oidswitchniccreate"></a>OID\_スイッチ\_NIC\_を作成します。


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_を作成して拡張可能スイッチ拡張機能を基になる新しい接続が確立されていることを通知するには拡張可能スイッチ ポートと外部接続または仮想ネットワーク アダプターの間 拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行して、接続が完全に確立されると、 [OID\_切り替える\_NIC\_CONNECT](oid-switch-nic-connect.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_切り替える\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造の拡張可能スイッチのポートを指定しますこの作成の通知が行わします。 拡張可能スイッチ拡張機能の OID クエリ要求を発行して拡張可能スイッチには、これと他のポートのパラメーター情報を取得できます[OID\_切り替える\_ポート\_配列](oid-switch-port-array.md)します。

**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体は、ネットワーク アダプターのインデックスを指定します。対象の作成の通知が行われました。 指定したネットワーク アダプター**インデックス**値がで指定された拡張可能スイッチ ポートに接続されている、 **PortId**メンバー。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)します。

OID の OID のセット要求を受け取ったとき\_スイッチ\_NIC\_作成、拡張機能には、次のガイドラインが従う必要があります。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) OID 要求に関連付けられている構造体。

-   OID\_切り替える\_NIC\_に通知が表示されている、新しい接続を拡張可能スイッチ拡張機能のみを要求の作成、そのパケット トラフィック可能性があります、指定したポートが行われるように間もなく開始されます。 ただし、拡張機能ポートを使用できませんの OID セット要求を発行する拡張可能スイッチのプロトコルの端まで[OID\_切り替える\_NIC\_CONNECT](oid-switch-nic-connect.md)します。 その OID が発行されるまで、拡張機能は以下を実行する必要があります。

    -   拡張可能スイッチ ポートでのネットワーク アダプターの接続にパケット トラフィックを生成、OID\_切り替える\_NIC\_OID の作成要求が発行します。

    -   転送するかの OID 要求を発信[OID\_スイッチ\_NIC\_要求](oid-switch-nic-request.md)を基になるネットワーク アダプターに OID\_スイッチ\_NIC\_OID の作成要求が発行されました。

    -   転送するか元の状態インジケーターの NDIS [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)を基になるネットワーク アダプターからOID\_スイッチ\_NIC\_OID の作成要求が発行されています。

    -   呼び出す[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)拡張可能スイッチ ポートで指定されたネットワーク アダプター接続の拡張可能スイッチの参照カウンターをインクリメントします。

    **注**  、拡張機能の送信をインターセプトまたは OID の OID 要求間で指定したポートのパケットの受信が\_スイッチ\_NIC\_作成と[OID\_スイッチ\_NIC\_CONNECT](oid-switch-nic-connect.md)します。 この場合、拡張機能は、送信転送したり、それらのキャンセルではなく要求をパケットを受信しないでください。

     

-   拡張機能は、NDIS を返すことによって作成の通知を拒否できます\_状態\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、指定したポートで構成されているそのポリシーを満たすことができない、拡張機能は作成の通知を拒否する必要があります。

    拡張機能は、その他の NDIS を返す場合\_状態\_*Xxx*ステータス コードを作成の通知が拒否されることもできます。 ただし、NDIS を返すなどの一時的なシナリオに関する状態コードを返す\_状態\_リソースが作成の通知の再試行になる可能性があります。

    場合は、拡張機能が、OID 要求を拒否しては、要求が完了したときに、状態を監視する必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

    **注**  場合、拡張機能は、OID 要求を拒否のみできます、**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造が 0 のネットワーク アダプターのインデックス値を指定します。

     

-   呼び出す必要がありますが、拡張機能は、作成の通知を拒否していない場合、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張可能スイッチ ドライバー スタックの拡張機能を基になるには、この OID 要求を転送します。

    **注**  拡張機能は、この OID 要求の完了ステータスを監視する必要があります。 拡張機能は、拡張可能スイッチ ドライバー スタック内の基になる拡張機能の作成の通知が拒否されたかどうかを検出します。

     

-   拡張機能を呼び出す場合[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)この OID 要求を転送するように、拡張機能がすぐにパケット トラフィックを受信またはから、拡張可能なスイッチ ポート。 さらに、拡張機能が送信を挿入するすぐに、または、拡張可能スイッチ ポートのトラフィックを受信できません。

-   拡張可能スイッチのプロトコルのエッジの OID セットの要求を発行した後、拡張機能は拡張可能スイッチ ポートにパケット トラフィックを転送のみできます[OID\_切り替える\_NIC\_CONNECT](oid-switch-nic-connect.md)します。

    **注**  状況によっては、パケット トラフィック転送されますが、拡張可能なスイッチ ポートに OID の要求を設定する前に[OID\_切り替える\_NIC\_CONNECT](oid-switch-nic-connect.md)発行されます。

     

-   拡張可能スイッチの外部ネットワーク アダプターは、1 つまたは複数の基になる物理アダプターにバインドできます。 拡張可能スイッチのプロトコルのエッジが OID の独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべての物理ネットワーク アダプターの\_切り替える\_NIC\_作成します。 各 OID セットの要求では、別のネットワーク アダプター接続のインデックス値を指定します。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)します。

    拡張機能では、基になる各物理アダプターの接続状態を維持する必要があります。 外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)します。

拡張可能スイッチ ポートとネットワーク アダプターの接続の状態の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。

**注**  、拡張機能は、OID の独自の OID セット要求を発行する必要があります\_スイッチ\_NIC\_作成します。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張機能の OID OID セットの要求が完了すると\_スイッチ\_NIC\_作成で、1 つを返しますの次のステータス コード。

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

 

拡張機能は OID の OID のセット要求を完了しない場合\_切り替える\_NIC\_拡張可能スイッチの基になるミニポート端で作成、要求が完了します。 基になるミニポート edge には、この OID セットの要求の次のステータス コードが返されます。

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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_接続](oid-switch-nic-connect.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




