---
title: OID_RECEIVE_FILTER_FREE_QUEUE
description: NDIS プロトコルドライバーは、RECEIVE キューを解放するために、OID_RECEIVE_FILTER_FREE_QUEUE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: ee8cff69-2f5e-4798-9c18-28e996dd1dd4
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_FREE_QUEUE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d63764fa3fa4b896b731ad788661b210fb02e5d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844015"
---
# <a name="oid_receive_filter_free_queue"></a>OID\_受信\_フィルター\_空き\_キュー


NDIS プロトコルドライバーは、オブジェクト識別子 (OID) を設定する OID の要求\_受信\_フィルター\_空き\_キューを取得して、受信キューを解放します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_queue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)に対するポインターが含まれています。これには、型のキュー識別子を使用して、無料\_パラメーター構造が含まれます。**NDIS\_\_キュー\_ID を受信**します。

<a name="remarks"></a>注釈
-------

Oid\_\_フィルター\_\_受信する oid セット要求は、NDIS 6.20 以降のミニポートドライバーでは省略可能です。 バーチャルマシンキューインターフェイスをサポートするミニポートドライバーでは必須です。

その後のドライバーが[\_フィルターを受け取る oid\_受信](oid-receive-filter-allocate-queue.md)し、受信キューを割り当てるために\_キュー OID を割り当てる\_、oid を発行\_キュー OID\_解放して受信を解放します。再生.

NDIS は、VMQ 受信キューを解放するようにミニポートドライバーを要求するときに、次の手順を実行します。

1.  ネットワークアダプターは、受信キューに関連付けられているバッファーを受信するために、データの DMA 転送を停止します。その後、キューは DMA 停止状態になる必要があります。 ネットワークアダプターは、Oid を受信したときに DMA アクティビティを停止したことがあります。 [\_受信\_\_フィルターをクリア\_フィルター](oid-receive-filter-clear-filter.md) oid 要求を受信して、受信キューの最後の set フィルターをクリアします。

2.  ミニポートドライバーによって、ndis\_の状態[ **\_受信\_\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)の状態が表示されます。これには、 [**ndis\_receive\_queue\_state**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state) Structure set の**queuestate**メンバーが含まれます。**NdisReceiveQueueOperationalStateDmaStopped**に、DMA 転送が停止されたことを NDIS に通知します。

3.  ミニポートドライバーは、そのキューのすべての受信パケットがミニポートドライバーに返されるまで待機します。

4.  ミニポートドライバーは、 [**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)を呼び出すことによって、キューに関連付けられているネットワークアダプターの受信バッファーに割り当てられたすべての共有メモリを解放します。

5.  ミニポートドライバーは、receive キューを解放するために、\_QUEUE OID 要求\_\_フィルターの\_を受信する OID を完了します。

ミニポートドライバーは、 [**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)関数を呼び出して、キューの共有メモリを解放します。 ミニポートドライバーによって既定以外のキューの共有メモリが割り当てられている場合、ドライバーは、キューを解放している間に\_キュー OID を解放\_\_フィルターを使用して、共有メモリを OID のコンテキスト\_解放します。 ミニポートドライバーは、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数のコンテキストで既定のキューに割り当てられた共有メモリを解放します。

後続のドライバーは、キューを解放する前に、キューに設定されているすべてのフィルターを解放する必要があります。 また、 [**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)関数を呼び出してネットワークアダプターへのバインドを閉じる前に、ネットワークアダプターに割り当てられているすべての受信キューを解放する必要があります。 NDIS は、ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出す前に、ネットワークアダプターに割り当てられているすべてのキューを解放します。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、この要求に対して次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポートドライバーが要求を正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポートドライバーは、要求を非同期的に完了します。 ミニポートドライバーはすべての処理を完了した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>関数を呼び出し、 <em>STATUS</em>パラメーターに<strong>NDIS_STATUS_SUCCESS</strong>を渡すことによって、要求を成功させる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポートドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポートドライバーが要求の処理を停止しました。 たとえば、NDIS は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>Miniportresetex</em></a>関数を呼び出しました。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求に対して次のいずれかの状態コードを返します。

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
<td><p>要求されたキューが正常に解放されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>キュー id が無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS は<strong>データ</strong>を設定します。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、 <strong>bytesneeded 必要</strong>です。</p></td>
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


[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_\_QUEUE\_FREE\_パラメーターを受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)

[**NDIS\_ステータス\_\_キュー\_状態を受信します**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)

[OID\_受信\_フィルター\_割り当て\_キュー](oid-receive-filter-allocate-queue.md)

 

 




