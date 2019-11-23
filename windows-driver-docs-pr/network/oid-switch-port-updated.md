---
title: OID_SWITCH_PORT_UPDATED
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートの更新について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PORT_UPDATED に発行します。
ms.assetid: 7FDC963A-92E4-49B2-AB77-FA9C92EEBC25
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SWITCH_PORT_UPDATED
ms.localizationpriority: medium
ms.openlocfilehash: 85ca05120af6b5e93967db03b59fad6a1613684c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843921"
---
# <a name="oid_switch_port_updated"></a>OID\_スイッチ\_ポート\_更新されました


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セット要求 OID\_スイッチ\_\_ポートが更新され、拡張可能なスイッチポートの更新について拡張可能スイッチ拡張機能に通知します。 OID は、既に作成されていて、破棄/削除プロセスを開始していないポートに対してのみ発行されます。 現時点では、 **Portfriendlyname**フィールドのみが、作成後に更新されることがあります。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造が保存されます。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_port\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造体の**ポート id**メンバーは、更新通知を実行する拡張可能なスイッチポートを指定します。

この拡張機能は、次のガイドラインに従って、OID\_スイッチ\_ポート\_更新された OID セット要求を処理する必要があります。

-   拡張機能では、OID 要求に関連付けられている[**ポート\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)を変更することはできません。

-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を失敗させることはできません。

**注**拡張可能なスイッチ拡張機能  OID の oid セット要求を発行しないでください\_スイッチ\_ポート\_更新しました。

 

拡張可能なスイッチポートとネットワークアダプター接続の状態の詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_ポート\_更新された OID セット要求を完了し、次のステータスコードを返します。

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

[**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_スイッチ\_NIC\_削除](oid-switch-nic-delete.md)

[OID\_スイッチ\_ポート\_配列](oid-switch-port-array.md)

[*上書き/Nic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




