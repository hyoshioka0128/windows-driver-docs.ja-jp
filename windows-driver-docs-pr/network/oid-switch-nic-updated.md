---
title: OID_SWITCH_NIC_UPDATED
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、OID_SWITCH_NIC_UPDATED のオブジェクト識別子 (OID) セット要求を拡張可能なスイッチドライバースタックに発行します。
ms.assetid: C1B446A3-861F-41B4-99EF-C7CB45F86F39
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_NIC_UPDATED ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 1b2e8e5bd806e8ce87f10a797bd6e972f2529996
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843941"
---
# <a name="oid_switch_nic_updated"></a>OID\_スイッチ\_NIC\_更新されました


Hyper-v 拡張可能スイッチのプロトコルエッジは、OID\_スイッチ\_NIC のオブジェクト識別子 (OID) セット要求を発行し、\_拡張可能なスイッチドライバースタックに更新します。 この OID 要求は、ネットワークアダプターのパラメーターの更新について、基になる拡張可能なスイッチ拡張機能に通知します。 OID は、既に接続されていて、切断プロセスを開始していない Nic に対してのみ発行されます。 これらの実行時構成の変更には、 **NicFriendlyName**、 **netcfginstanceid**、 **MTU**、 **numPermanentMacAddress deid**、、 **vmmacaddress**、 **currentmacaddress**、および vfassigned を含めることができます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**ポート id**メンバーは、更新通知を行うポートを指定します。 拡張可能なスイッチ拡張機能では、 [oid\_スイッチ\_ポート\_配列](oid-switch-port-array.md)の oid クエリ要求を発行することによって、拡張可能スイッチ上のこのポートとその他のポートのパラメーター情報を取得できます。

[**NDIS\_スイッチ\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体の**インデックス**メンバーは、更新通知を行うネットワークアダプターのインデックスを指定します。 指定された**インデックス**値を持つネットワークアダプターは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されています。 これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)」を参照してください。

この拡張機能は、次のガイドラインに従って OID\_スイッチ\_\_NIC のセット要求を処理する必要があります。

-   この拡張機能では、OID 要求に関連付けられている[**NIC\_パラメーター構造\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)を変更することはできません。
-   拡張機能は、常にこの OID セット要求を基になる拡張機能に転送する必要があります。 拡張機能は要求を完了できません。
-   拡張機能は、OID\_スイッチ\_NIC\_更新された独自の OID セット要求を発行してはなりません。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチの OID クエリ要求を完了し\_NIC\_更新し、次のステータスコードを返します。

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

 

 




