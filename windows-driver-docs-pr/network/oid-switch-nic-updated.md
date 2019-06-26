---
title: OID_SWITCH_NIC_UPDATED
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、拡張可能スイッチのドライバー スタックを OID_SWITCH_NIC_UPDATED のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: C1B446A3-861F-41B4-99EF-C7CB45F86F39
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_UPDATED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 961da96e3927cc093e9f5b945c466dd18bb5f087
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366574"
---
# <a name="oidswitchnicupdated"></a>OID\_スイッチ\_NIC\_更新日


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_拡張可能スイッチのドライバー スタックを更新します。 この OID 要求では、ネットワーク アダプターのパラメーターの更新プログラムの拡張可能スイッチの拡張機能を基になるに通知します。 OID は、Nic が接続された既にを切断プロセスを開始していないに対してのみ発行されます。 これらの実行時の構成変更を含めることができます**NicFriendlyName**、 **NetCfgInstanceId**、 **MTU**、 **NumaNodeId**、 **PermanentMacAddress**、 **VMMacAddress**、 **CurrentMacAddress**、および**VFAssigned**します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体。

<a name="remarks"></a>注釈
-------

**PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造では、ポートを指定する、更新プログラム通知が行わします。 拡張可能スイッチ拡張機能の OID クエリ要求を発行して拡張可能スイッチには、これと他のポートのパラメーター情報を取得できます[OID\_切り替える\_ポート\_配列](oid-switch-port-array.md)します。

**インデックス**のメンバー、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)構造体は、ネットワーク アダプターのインデックスを指定します。対象の更新の通知が行われました。 指定したネットワーク アダプター**インデックス**値がで指定された拡張可能スイッチ ポートに接続されている、 **PortId**メンバー。 これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)します。

拡張機能は、OID の要求を設定する OID の処理の次のガイドラインに従う必要があります\_スイッチ\_NIC\_更新日。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) OID 要求に関連付けられている構造体。
-   拡張機能では、基になる拡張機能をこの OID セット要求を常に転送する必要があります。 拡張機能は、要求を完了する必要があります。
-   拡張機能は、OID の独自の OID セット要求を発行する必要があります\_スイッチ\_NIC\_更新されました。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_更新し、次のステータス コードを返します。

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

 

 




