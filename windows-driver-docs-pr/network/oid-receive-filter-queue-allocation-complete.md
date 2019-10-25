---
title: OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE
description: NDIS プロトコルドライバーは、OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE のオブジェクト識別子 (OID) メソッドの要求を発行して、受信キューの現在のバッチに割り当てが完了したことをミニポートドライバーに通知します。
ms.assetid: d09fcab5-4c3b-432a-ba9e-fd4269537de6
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 397f802e24f844bc2a45049acb91deed9fc3d3e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843999"
---
# <a name="oid_receive_filter_queue_allocation_complete"></a>OID\_受信\_フィルター\_キュー\_割り当て\_完了


NDIS プロトコルドライバーは、オブジェクト識別子 (OID) メソッドの OID 要求を受信\_フィルター\_キュー\_割り当て\_完了し、現在の受信バッチの割り当てが完了したことをミニポートドライバーに通知\_ます。行列.

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)へのポインターが含まれています\_割り当て\_完全な\_配列構造を格納します。次に、 [**NDIS\_受信\_キュー\_割り当て\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters) 、各キューの\_パラメーター構造を完了します。 OID メソッド要求から正常に返された後、 **NDIS\_oid\_要求**構造の**informationbuffer**メンバーには、構造体の同じ配列へのポインター**と、各** **NDIS\_受信\_キュー\_割り当て\_完了\_パラメーター**構造には、各キューの完了状態が含まれます。

<a name="remarks"></a>注釈
-------

Oid\_\_フィルター\_キュー\_割り当て\_完了を受信する oid メソッド要求は、NDIS 6.20 以降のミニポートドライバーでは省略可能です。 バーチャルマシンキュー (VMQ) インターフェイスをサポートするミニポートドライバーでは必須です。

1つ以上の受信キューを割り当て、必要に応じて初期フィルターを設定した後、プロトコルドライバーは oid\_\_の OID メソッド要求を発行する必要があります。これにより、\_キュー\_割り当て\_完了して、受信キューの現在のバッチに対して割り当てが完了したミニポートドライバー。 これにより、ミニポートドライバーは複数の受信キュー間でハードウェアリソースのバランスを取ることができます。必要に応じて、受信キューの共有メモリなどのリソースを割り当てることができます。

ミニポートドライバーが\_OID を受信した後\_フィルター\_キュー\_割り当て\_要求を完了し、キューに設定されたフィルターがある場合、キューは実行中の状態になります。 この状態では、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによって、ミニポートドライバーがキュー内のパケットの兆候を開始できます。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーは、oid の OID メソッド要求について、次のいずれかの状態コードを返します。\_受信\_フィルター\_キュー\_割り当て\_完了します。

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
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>キューの割り当てが完了しました。 情報バッファーには、更新された<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)"><strong>NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY</strong></a>構造体と、キュー割り当ての完了ステータスを含むパラメーター構造が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>要求は完了待ちです。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>指定された1つ以上のパラメーターが有効ではありませんでした。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS は<strong>データ</strong>を設定します。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、 <strong>bytesneeded 必要</strong>です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>ミニポートドライバーの NDIS バージョンは、バージョン6.20 より前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
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


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_キュー\_割り当て\_完了\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)

[**NDIS\_受信\_キュー\_割り当て\_完了\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)

 

 




