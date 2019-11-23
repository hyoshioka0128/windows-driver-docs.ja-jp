---
title: OID_QOS_CURRENT_CAPABILITIES
description: このドライバーは、ネットワークアダプターの現在有効なサービス品質 (QoS) ハードウェア機能を取得するために、OID_QOS_CURRENT_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: E9013EB2-5EDB-4BCB-BC1D-17345B85D1C4
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_QOS_CURRENT_CAPABILITIES
ms.localizationpriority: medium
ms.openlocfilehash: e9528517a8367b1acefbc08fbfed9f3f5cc1a2af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844031"
---
# <a name="oid_qos_current_capabilities"></a>OID\_QOS\_現在の\_機能


その後のドライバーは、OID\_のオブジェクト識別子 (OID) クエリ要求を使用して、現在有効になっているネットワークアダプターのサービス品質 (QoS) ハードウェア機能を取得するために、現在の\_機能を\_します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_QOS\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造体へのポインターが含まれています。

この OID クエリ要求は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバー用に NDIS によって処理される  に**注意**してください。

 

<a name="remarks"></a>注釈
-------

ミニポートドライバー [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されると、ネットワークアダプターの現在有効な NDIS QoS ハードウェア機能が登録されます。 ドライバーは、次の手順に従ってこれらの機能を登録します。

1.  このドライバーは、有効になっている QoS ハードウェア機能を使用して、 [**NDIS\_qos\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造を初期化します。

2.  このドライバーは、ndis [ **\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の**CurrentQosCapabilities**メンバーを設定し、\_属性構造を[**ndis\_QOS\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造体へのポインターに\_\_します。

3.  次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

**注**  ndis は、バインドまたはアタッチ操作中に、ネットワークアダプターの現在有効になっている ndis QoS ハードウェア機能を、後続のプロトコルおよびフィルタードライバーに報告しません。

 

NDIS QoS 機能の登録方法の詳細については、「 [Ndis Qos 機能の登録](https://docs.microsoft.com/windows-hardware/drivers/network/registering-ndis-qos-capabilities)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID\_の oid クエリ要求を、ミニポートドライバーに対する現在の\_機能要求\_処理し、次のステータスコードのいずれかを返します。

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
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポートドライバーは、NDIS QoS インターフェイスをサポートしていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)"><strong>NDIS_QOS_CAPABILITIES</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

 

 




