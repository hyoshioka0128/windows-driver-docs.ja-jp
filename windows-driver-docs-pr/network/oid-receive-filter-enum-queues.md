---
title: OID_RECEIVE_FILTER_ENUM_QUEUES
description: その後のドライバーとユーザーモードアプリケーションは、OID_RECEIVE_FILTER_ENUM_QUEUES のオブジェクト識別子 (OID) クエリ要求を発行して、ネットワークアダプターに割り当てられているすべての受信キューの一覧を取得します。
ms.assetid: e8a946a2-9ee9-42a0-8175-fbc592d404d1
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_ENUM_QUEUES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 08ea9859a59bb72af6a06eab9a732d32b8c55d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844013"
---
# <a name="oid_receive_filter_enum_queues"></a>OID\_受信\_フィルター\_列挙型\_キュー


その後のドライバーとユーザーモードアプリケーションは、OID のオブジェクト識別子 (OID) クエリ要求を発行\_、列挙型\_キューを受信\_フィルター\_処理して、ネットワークアダプターに割り当てられているすべての受信キューの一覧を取得します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_QUEUE\_INFO\_ARRAY へのポインターが含まれています。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)各フィルターの[ **\_QUEUE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)構造体を受け取る構造体の後に、NDIS\_によって受信されます。

<a name="remarks"></a>注釈
-------

NDIS は、Oid から受信したデータの内部キャッシュから情報を取得し、\_QUEUE と Oid を[割り当てる\_キュー](oid-receive-filter-allocate-queue.md)と OID を割り当てるために、\_フィルターを\_受信します。\_\_[フィルター\_パラメーター](oid-receive-filter-queue-parameters.md)OID 要求。

その後のドライバーとユーザーモードアプリケーションは、oid の OID クエリ要求を発行し、列挙型\_キューを受信\_フィルター\_して、ネットワークアダプターの受信キューを列挙\_します。

プロトコルドライバーが要求を発行すると、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造内の要求の種類が**NdisRequestQueryInformation**に設定されます。この oid は、プロトコルドライバーによって割り当てられたすべての受信キューの配列を返します。ネットワークアダプター上。 ユーザーモードアプリケーションが要求を発行した場合、 **NDIS\_oid\_要求**構造内の要求の種類が**NdisRequestQueryStatistics**に設定され、この oid は、のすべての受信キューに関する情報の配列を返します。ネットワークアダプター。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID の OID クエリ要求を処理します。これは、ミニポートドライバーの列挙型\_キューを受信\_フィルター\_\_、次のいずれかのステータスコードを返します。

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
<td><p>要求は正常に完了しました。 <strong>Informationbuffer</strong>は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)"><strong>NDIS_RECEIVE_QUEUE_INFO_ARRAY</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS は<strong>データ</strong>を設定します。<strong>METHOD_INFORMATION</strong>。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、 <strong>bytesneeded 必要</strong>です。</p></td>
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


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_RECEIVE\_QUEUE\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)

[**NDIS\_\_キュー\_情報\_配列を受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)

[OID\_受信\_フィルター\_割り当て\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_\_フィルター\_\_キューのパラメーターを受け取る](oid-receive-filter-queue-parameters.md)

 

 




