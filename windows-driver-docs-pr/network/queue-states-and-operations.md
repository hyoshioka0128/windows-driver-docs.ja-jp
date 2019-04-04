---
title: キューの状態と操作
description: キューの状態と操作
ms.assetid: 892f8f19-b94e-4950-af88-334c9a8b8c0d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b54e8cde586d4687a1092b31ee0402a64dc0c0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532212"
---
# <a name="queue-states-and-operations"></a>キューの状態と操作





キューごとにネットワーク アダプターは、次の操作状態のセットをサポートする必要があります。

<a href="" id="undefined"></a>未定義  
キューは割り当てられません。 上にある、ドライバーが送信キューを割り当てる、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784) OID 要求。

<a href="" id="allocated"></a>割り当てられました。  
*Allocated*状態は、キューの初期状態です。 上にあるドライバーが、キューではのフィルターを通常は設定するキューは、割り当てられている状態では、ときに、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) OID またはキューが完了します。割り当て、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID 要求。

<a href="" id="set"></a>設定  
*設定*状態では、キューに割り当てられている少なくとも 1 つのフィルターが、上にあるドライバーは送信されませんが、 [OID\_受信\_フィルター\_キュー\_の割り当て\_完全な](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID。

<a href="" id="running"></a>実行しています。  
*を実行している*状態では、キューにフィルター設定、キューの割り当てが完了し、ミニポート アダプターでは、キューのパケットの受信を示すです。

<a href="" id="paused"></a>一時停止  
*Paused*状態では、ネットワーク アダプターには、キューの受信ネットワーク データは示しません。 前に、キューに設定されているフィルターがなかったか、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)された OID 要求またはすべてのフィルターキューのセットのクリア、 [OID\_受信\_フィルター\_クリア\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785) OID 要求。

<a href="" id="dma-stopped"></a>DMA の停止  
*DMA 停止*状態では、受信したミニポート ドライバー、 [OID\_受信\_フィルター\_FREE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569789) OID 要求。 ときに、DMA が停止し、ドライバーが、DMA 停止の状態を示す値を発行 (と[ **NDIS\_状態\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567417))、ドライバーは解放の状態になります。

<a href="" id="freeing"></a>解放します。  
*解放*状態では、ミニポート ドライバーの送信を停止し、受信、キューの操作に必要な操作が完了して、関連付けられているリソースを解放します。 インジケーターが完了すると、未処理のすべての受信後に、キューが削除され、キューが未定義です。

次の表では、見出しは、キューの状態です。 主なイベントは、最初の列に表示されます。 テーブル内のエントリの残りの部分は、[次へ] を指定状態の特定の状態でイベントが発生した後、キューに入るようにします。 空のエントリは、無効なイベントの状態の組み合わせを表します。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント \ 状態</th>
<th align="left">未定義</th>
<th align="left">割り当てられました。</th>
<th align="left">設定</th>
<th align="left">実行中</th>
<th align="left">一時停止</th>
<th align="left">DMA を停止します。</th>
<th align="left">解放します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_ALLOCATE_QUEUE - メソッド (set)</p></td>
<td align="left"><p>割り当てられました。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS - メソッド (クエリ) の要求</p></td>
<td align="left"></td>
<td align="left"><p>割り当てられました。</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS のセットの要求</p></td>
<td align="left"></td>
<td align="left"><p>割り当てられました。</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_SET_FILTER - メソッド (set) 要求</p></td>
<td align="left"></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER のセットの要求 (最後のフィルター)</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>割り当てられました。</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER のセットの要求 (最後のないフィルター)</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_ENUM_FILTERS - メソッド (クエリ要求)</p></td>
<td align="left"></td>
<td align="left"><p>割り当てられました。</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_PARAMETERS - メソッド (クエリ) の要求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE - メソッド (set) 要求</p></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>パケットを受信します。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>実行中</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_FREE_QUEUE 要求の設定</p></td>
<td align="left"></td>
<td align="left"><p>DMA を停止します。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>DMA を停止します。</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DMA を停止および NDIS_STATUS_RECEIVE_QUEUE_STATE 状態を示す値を送信した (注。DMA が、割り当て済みでおそらく既に停止しているか、状態を一時停止)</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>解放します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>すべての受信が完了し、キュー リソースの解放がないです。</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>未定義</p></td>
</tr>
</tbody>
</table>

 

**注**  上記の表に示したイベントには、状態の変更が発生しない一部のセカンダリ イベントが含まれます。 これらのイベントが有効な状態を指定するテーブルには、これらのセカンダリ イベントが含まれます。

 

プライマリ キュー イベントの定義は次のとおりです。

<a href="" id="oid-receive-filter-allocate-queue---method--set--request"></a>OID\_受信\_フィルター\_ALLOCATE\_キュー - 要求のメソッド (set)  
上位のドライバーには、キューが割り当てられます。 キューの割り当てに関する詳細については、[割り当てと解放 VM キュー](allocating-and-freeing-vm-queues.md)を参照してください。

<a href="" id="oid-receive-filter-set-filter---method--set--request"></a>OID\_受信\_フィルター\_設定\_フィルター - メソッド (set) 要求  
上にある、ドライバーは、キューに対してフィルターを設定します。 上にあるドライバーが送信されていない場合、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID、状態の設定、キューが。 それ以外の場合、キューは、実行状態です。 キューのフィルターの設定に関する詳細については、[設定および VMQ のフィルターをクリアする](setting-and-clearing-vmq-filters.md)を参照してください。

<a href="" id="oid-receive-filter-clear-filter---set-request"></a>OID\_受信\_フィルター\_クリア\_フィルターのセットの要求  
上位のドライバーには、キューにフィルターがクリアされます。 実行中のキューの最後のフィルターをオフにした場合、DMA を停止することができます。表示されるインジケーターは停止され、存在する場合、受信したデータのキューをクリアする必要があります。 詳細については、キューにフィルターをオフにすると、[設定および VMQ のフィルターをクリアする](setting-and-clearing-vmq-filters.md)を参照してください。

<a href="" id="oid-receive-filter-queue-allocation-complete---method--set--request"></a>OID\_受信\_フィルター\_キュー\_割り当て\_メソッド (set) の要求の完了  
上位のドライバーには、キューの割り当てが完了しました。 実行では、状態し、受信がキューに設定されているフィルターがある場合は、問題を開始できます。 キューの割り当てを完了する詳細については、[割り当てと解放 VM キュー](allocating-and-freeing-vm-queues.md)を参照してください。

<a href="" id="receive-packet"></a>パケットを受信します。  
ミニポート ドライバーを示すことができますのみが実行状態にあるキューのパケットを受信します。 キューのかを示す受信したデータの詳細については、[VMQ の送信と受信操作](vmq-send-and-receive-operations.md)を参照してください。

<a href="" id="oid-receive-filter-free-queue-set-request-"></a>OID\_受信\_フィルター\_FREE\_キューが要求を設定します。  
上にある、ドライバーは、キューを解放します。 ドライバーは、DMA 停止の状態を示す値を発行 (と[ **NDIS\_状態\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567417))、ドライバーが、解放を入力状態。 未処理のすべての受信の表示が完了とキュー リソースが解放されます、キューが定義されていません。

 

 





