---
title: OID_RECEIVE_FILTER_MOVE_FILTER
description: 上にある、ドライバーは、以前に構成された受信のフィルターを移動する OID_RECEIVE_FILTER_MOVE_FILTER のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: CC899ABD-EE6B-4932-889F-984C8B5A403F
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_MOVE_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ef8a1446d655f7d3cdf9f4aacdc8245497485e8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384208"
---
# <a name="oidreceivefiltermovefilter"></a>OID\_受信\_フィルター\_移動\_フィルター


上位のドライバーの OID オブジェクト識別子 (OID) セット要求を発行する\_受信\_フィルター\_移動\_以前に構成された受信のフィルターを移動するフィルター。 受信フィルターは、1 つの仮想ポート (VPort) から異なる VPort に移動されます。

上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID セット要求を発行します。 この OID セットの要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)構造体。

<a name="remarks"></a>注釈
-------

NDIS のメンバーの検証、 [ **NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)前に構造体転送、OID は、PF ミニポート ドライバーに要求を設定します。

PF のミニポート ドライバーでは、アトミックにこの OID セット要求を処理する必要があります。 ドライバーは、同時に受信キューと VPort からフィルターを削除し、別の受信キューと VPort に設定するには、ネットワーク アダプターを構成できる必要があります。

詳細については、次を参照してください。[仮想ポートに受信フィルターを移動](https://docs.microsoft.com/windows-hardware/drivers/network/moving-a-receive-filter-to-a-virtual-port)します。

### <a name="return-status-codes"></a>リターン状態コード

OID OID の要求の設定の次のステータス コードのいずれかの PF ミニポート ドライバー返します\_受信\_フィルター\_移動\_フィルター。

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
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"> <strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
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

[**NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)

 

 




