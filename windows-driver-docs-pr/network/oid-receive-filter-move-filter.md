---
title: OID_RECEIVE_FILTER_MOVE_FILTER
description: 前に構成された受信フィルターを移動するために、OID_RECEIVE_FILTER_MOVE_FILTER のオブジェクト識別子 (OID) セット要求が発生します。
ms.assetid: CC899ABD-EE6B-4932-889F-984C8B5A403F
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_MOVE_FILTER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 13a1043f27bc4dfbfd91e24cadcf381c3de5c433
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844006"
---
# <a name="oid_receive_filter_move_filter"></a>OID\_受信\_フィルター\_移動\_フィルター


前に構成された受信フィルターを移動するために\_フィルターを移動\_には、\_\_OID のオブジェクト識別子 (OID) セット要求が発生すると、その後のドライバーで問題が発生します。 受信フィルターは、1つの仮想ポート (VPort) から別の VPort に移動されます。

この OID セット要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 この OID セット要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)\_\_パラメーター構造へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS は、OID セット要求を PF ミニポートドライバーに転送する前に[ **\_\_フィルター\_パラメーター構造を受け取るために、ndis\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)のメンバーを検証します。

PF ミニポートドライバーは、この OID セット要求をアトミックに処理する必要があります。 ドライバーは、受信キューと VPort からフィルターを同時に削除し、別の受信キューと VPort に設定するように、ネットワークアダプターを構成できる必要があります。

詳細については、「[受信フィルターを仮想ポートに移動する](https://docs.microsoft.com/windows-hardware/drivers/network/moving-a-receive-filter-to-a-virtual-port)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、oid の OID セット要求に対して次のいずれかの状態コードを返します。\_フィルター\_移動\_フィルターを\_受信します。

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
<td><p>PF ミニポートドライバーは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>) 未満です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="odd">
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_フィルター\_のフィルター\_パラメーターの\_移動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)

 

 




