---
title: OID_NIC_SWITCH_CURRENT_CAPABILITIES
description: ネットワークアダプターの NIC スイッチで現在有効になっているハードウェア機能を取得するために、OID_NIC_SWITCH_CURRENT_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求が、その後のドライバーによって発行されます。
ms.assetid: 529dc5d5-9b84-4891-9e7a-1f9f7850c6d7
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_CURRENT_CAPABILITIES
ms.localizationpriority: medium
ms.openlocfilehash: f1bf011e3ec836f322bea55a6567f006a743859b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844095"
---
# <a name="oid_nic_switch_current_capabilities"></a>OID\_NIC\_スイッチ\_現在の\_機能


その後のドライバーは、OID\_NIC\_\_スイッチのオブジェクト識別子 (OID) クエリ要求を発行し、現在の\_機能を使用して、ネットワークアダプターの NIC スイッチで現在有効になっているハードウェア機能を取得します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 6.20 以降、ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ネットワークアダプターで現在有効になっている NIC スイッチのハードウェア機能を提供します。 このドライバーは、NIC スイッチのハードウェア機能を使用して、\_の機能構造を[ **\_スイッチの\_nic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)を初期化し、NDIS [ **\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の**CURRENTNICSWITCHCAPABILITIES**メンバーを**ndis\_NIC\_スイッチ\_** の構造体へのポインターに設定します。\_\_\_ 次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを**NDIS\_ミニポート\_アダプター**へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

**注**  NDIS 6.30 以降では、シングルルート i/o 仮想化 (sr-iov) インターフェイスをサポートするミニポートドライバーは、NIC スイッチの有効なハードウェア機能を登録する必要があります。 ドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出すことによってこれらの機能を登録します。

 

プロトコルおよびフィルタードライバーは、OID\_NIC の OID クエリ要求を発行する必要はありません\_スイッチ\_現在の\_機能。 NDIS では、次のように、ネットワークアダプターの現在有効になっている NIC スイッチのハードウェア機能をこれらのドライバーに提供します。

-   NDIS は、バインド操作中に、基になるネットワークアダプターの現在有効に**なっている**NIC スイッチのハードウェア機能を、 [**ndis\_バインド\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造内のプロトコルドライバーに報告します。

-   NDIS は、基になるネットワークアダプターの現在有効になっている NIC スイッチのハードウェア機能を、 [**ndis\_フィルター\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)アタッチ操作中に\_PARAMETERS 構造体に接続**するため**のフィルタードライバーに報告します。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID\_NIC\_スイッチの OID クエリ要求を処理し、ミニポートドライバーに対する現在の\_機能要求を\_します。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_NIC を処理するときに、現在の\_機能の要求\_\_スイッチは、次のいずれかの状態コードを返します。

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
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>) 未満です。 ミニポートドライバーはデータを設定する必要があり<strong>ます。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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

[**NDIS\_フィルター\_\_パラメーターをアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




