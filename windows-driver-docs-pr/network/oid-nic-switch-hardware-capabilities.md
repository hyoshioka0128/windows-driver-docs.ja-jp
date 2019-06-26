---
title: OID_NIC_SWITCH_HARDWARE_CAPABILITIES
description: 上にある、ドライバーは、ネットワーク アダプターで NIC スイッチのハードウェア機能を取得する OID_NIC_SWITCH_HARDWARE_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 2c417a16-68e1-4754-88a5-8bac4653e05d
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 17cb6c96d63fbc46fd75ce6c989db5f4b452b41d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383665"
---
# <a name="oidnicswitchhardwarecapabilities"></a>OID\_NIC\_スイッチ\_ハードウェア\_機能


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_NIC\_切り替える\_ハードウェア\_NIC のハードウェア機能を取得する機能は、ネットワーク アダプターで切り替えます。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

<a name="remarks"></a>注釈
-------

[ **NDIS\_NIC\_切り替える\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体には、NIC のスイッチのネットワーク アダプターのハードウェア性能に関する情報が含まれています。 これらの機能は、INF ファイルの設定、または、現在無効になっているハードウェア機能を含めることができます、**詳細**プロパティ ページ。

**注**  の OID の OID クエリ要求によって指定された NIC スイッチのすべての機能が返されます\_NIC\_切り替える\_ハードウェア\_かどうかに関係なく、機能、機能を有効または無効になっています。

 

ミニポート ドライバー以降 NDIS 6.20 が動作では、NIC スイッチ ハードウェアの機能を提供時にその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数が呼び出されます。 ドライバーの初期化、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体の NIC にハードウェアの機能およびセットのスイッチ、 **HardwareNicSwitchCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体へのポインターを**NDIS\_NIC\_スイッチ\_機能**構造体。 ミニポート ドライバーを呼び出して、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数とセット、 *MiniportAttributes*パラメーターへのポインターを**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**構造体。

**注**  NDIS 6.30 以降、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするミニポート ドライバーは、NIC のスイッチのハードウェア機能を登録する必要があります。 ドライバーは、呼び出すことによってこれらの機能を登録[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

 

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_NIC\_スイッチ\_ハードウェア\_ミニポート ドライバー、および次のステータス コードを返します。 1 つの機能要求。

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
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>)。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

 

 




