---
title: OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE
description: NDIS プロトコル ドライバーは、オブジェクト識別子 OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE のミニポート ドライバーの受信キューの現在のバッチの割り当てが完了したことを通知する (OID) のメソッドを要求を発行します。
ms.assetid: d09fcab5-4c3b-432a-ba9e-fd4269537de6
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 56e85dd697cae5aac2d529408289cc958341cfc8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356127"
---
# <a name="oidreceivefilterqueueallocationcomplete"></a>OID\_受信\_フィルター\_キュー\_割り当て\_完了


NDIS プロトコル ドライバー発行オブジェクト識別子 (OID) メソッドの要求の OID\_受信\_フィルター\_キュー\_割り当て\_割り当てが完了したこと、ミニポート ドライバーに通知する完了受信キューの現在のバッチ。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_キュー\_割り当て\_完了\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)が続く構造体、 [ **NDIS\_受信\_キュー\_割り当て\_完了\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)キューごとに構造体。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造には同じ配列へのポインターが含まれています構造体、および**CompletionStatus**のそれぞれに所属**NDIS\_受信\_キュー\_割り当て\_完了\_パラメーター**構造体には、各キューの完了ステータスが含まれています。

<a name="remarks"></a>注釈
-------

OID の OID メソッド要求\_受信\_フィルター\_キュー\_割り当て\_完了は、NDIS 6.20 が動作し、それ以降のミニポート ドライバーでは省略可能。 仮想マシン キュー (VMQ) インターフェイスをサポートするミニポート ドライバーに対して必要があります。

割り当て後に 1 つ以上受信キューと最初のフィルターを必要に応じて設定するには、プロトコル ドライバーは OID の OID メソッド要求を発行する必要があります\_受信\_フィルター\_キュー\_割り当て\_ミニポート ドライバーの受信キューの現在のバッチの割り当てが完了したことを通知するために完了します。 これにより、ミニポート ドライバー、ハードウェアのバランスを取る複数の間でリソースの受信キューです。必要に応じて、受信キューの共有メモリなどのリソースを割り当てる、ことができます。

ミニポート後は、ドライバーは OID を受け取ります。\_受信\_フィルター\_キュー\_割り当て\_がキューに設定されているフィルターの要求を完了し、キューが実行状態。 この状態で、ミニポート ドライバーは、呼び出すことによって、キューにあるパケットの兆候を開始できます[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_受信\_フィルター\_キュー\_割り当て\_完了します。

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
<td><p>キューの割り当てが完了しました。 情報バッファーが含まれていますが、更新された<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)"> <strong>NDIS_RECEIVE_QUEUE_ALLOCATION_COMPLETE_ARRAY</strong> </a>構造と、キューの割り当てを表す完了状態で、パラメーター構造体。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>完了待ちになっています。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されるされます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>1 つ以上の上にあるドライバーが提供されているパラメーターが無効でした。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ</strong>.<strong>METHOD_INFORMATION</strong>.<strong>BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>ミニポート ドライバーの NDIS バージョン 6.20 が動作のバージョンよりも前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
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


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_キュー\_割り当て\_完了\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_array)

[**NDIS\_受信\_キュー\_割り当て\_完了\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_allocation_complete_parameters)

 

 




