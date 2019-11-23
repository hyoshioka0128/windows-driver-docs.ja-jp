---
title: OID_NIC_SWITCH_HARDWARE_CAPABILITIES
description: このドライバーは、ネットワークアダプターの NIC スイッチのハードウェア機能を取得するために、OID_NIC_SWITCH_HARDWARE_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 2c417a16-68e1-4754-88a5-8bac4653e05d
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_HARDWARE_CAPABILITIES
ms.localizationpriority: medium
ms.openlocfilehash: abdf922c087b0861ed206d7616ef7ed8dd0ac12e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844081"
---
# <a name="oid_nic_switch_hardware_capabilities"></a>OID\_NIC\_スイッチ\_ハードウェア\_機能


このドライバーは、OID\_\_NIC のオブジェクト識別子 (OID) クエリ要求を発行し、ハードウェア\_機能\_、ネットワークアダプターの NIC スイッチのハードウェア機能を取得します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造には、ネットワークアダプターの nic スイッチのハードウェア機能に関する情報が含まれています。 これらの機能には、INF ファイルの設定によって現在無効になっているハードウェア機能や、 **[詳細設定**] プロパティページを含めることができます。

指定された NIC スイッチのすべての機能は、機能が有効になっているか無効になっているかに関係なく、oid\_NIC\_スイッチ\_ハードウェア\_機能の OID クエリ要求によって返さ**れ  ます**。

 

NDIS 6.20 以降では、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ミニポートドライバーが NIC スイッチのハードウェア機能を提供します。 このドライバーは、NIC スイッチのハードウェア機能を使用して、 [**ndis\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を初期化し、NDIS [ **\_ミニポート\_アダプター\_ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)のハードドライブの**機能**のメンバーを設定します。\_は、ndis **\_NIC\_スイッチ\_** の構造体へのポインターを\_ます。 次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを**NDIS\_ミニポート\_アダプター**へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

**注**  NDIS 6.30 以降では、シングルルート i/o 仮想化 (sr-iov) インターフェイスをサポートするミニポートドライバーは、NIC スイッチのハードウェア機能を登録する必要があります。 ドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出すことによってこれらの機能を登録します。

 

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID\_NIC の OID クエリ要求を処理し、ミニポートドライバーに対するハードウェア\_機能要求\_\_し、次のステータスコードのいずれかを返します。

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
<td><p>要求は正常に完了しました。 <strong>Informationbuffer</strong>は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポートドライバーがシングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




