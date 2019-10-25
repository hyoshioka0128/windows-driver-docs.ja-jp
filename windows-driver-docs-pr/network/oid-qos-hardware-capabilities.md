---
title: OID_QOS_HARDWARE_CAPABILITIES
description: このドライバーは、ネットワークアダプターの NDIS Quality of Service (QoS) ハードウェア機能を取得するために、OID_QOS_HARDWARE_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 50D93F3F-DEA0-4D7D-8866-4155EED8D8BC
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_QOS_HARDWARE_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 37ef7ffb5e07ed976a67246b12c8c4c2fc12780a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844029"
---
# <a name="oid_qos_hardware_capabilities"></a>OID\_QOS\_ハードウェア\_機能


ネットワークアダプターの NDIS Quality of Service (QoS) ハードウェア機能を取得するために、1つ前のドライバーが OID のオブジェクト識別子 (OID) クエリ要求を発行し、ハードウェア\_機能を\_\_します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_QOS\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造体へのポインターが含まれています。

この OID クエリ要求は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバー用に NDIS によって処理される  に**注意**してください。

 

<a name="remarks"></a>注釈
-------

[**Ndis\_qos\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造には、ネットワークアダプターの ndis QOS ハードウェア機能に関する情報が含まれています。 これらの機能には、現在 INF ファイルの設定によって無効になっているハードウェア機能や、 **[詳細設定**] プロパティページがあります。

**注**  ネットワークアダプターのすべての NDIS QoS ハードウェア機能は、機能が有効になっているか無効になっているかにかかわらず、OID\_QOS\_ハードウェア\_機能の oid クエリ要求によって返されます。

 

ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ネットワークアダプターの NDIS QoS ハードウェア機能を登録します。 ドライバーは、次の手順に従ってこれらの機能を登録します。

1.  このドライバーは、ndis QoS ハードウェア機能を使用して、 [**ndis\_QOS\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造を初期化します。

2.  このドライバーは、ndis [ **\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の**HardwareQosCapabilities**メンバーを設定し、\_の属性構造を[**NDIS\_の QOS\_機能へのポインターに\_\_します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造体。

3.  次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを NDIS\_ミニポート\_アダプターへのポインターに設定します[ **\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

**注**  ndis では、バインドまたはアタッチ操作中に、ネットワークアダプターの ndis QoS ハードウェア機能が、後続のプロトコルおよびフィルタードライバーに報告されません。

 

NDIS QoS 機能の登録方法の詳細については、「 [Ndis Qos 機能の登録](https://docs.microsoft.com/windows-hardware/drivers/network/registering-ndis-qos-capabilities)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID\_の oid クエリ要求を処理します。これは、ミニポートドライバーに対するハードウェア\_機能の要求\_ハードウェアの要求で、次のいずれかのステータスコードを返します。

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
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)"><strong>NDIS_QOS_CAPABILITIES</strong></a>) 未満です。 NDIS はデータを設定<strong>します。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

 

 




