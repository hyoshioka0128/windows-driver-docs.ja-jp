---
title: OID_RECEIVE_FILTER_FREE_QUEUE
description: NDIS プロトコル ドライバーでは、受信キューを解放する OID_RECEIVE_FILTER_FREE_QUEUE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: ee8cff69-2f5e-4798-9c18-28e996dd1dd4
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_FREE_QUEUE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 17482b9a41a0960addebfc8784e116fb0bb5b4e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359150"
---
# <a name="oidreceivefilterfreequeue"></a>OID\_受信\_フィルター\_FREE\_キュー


OID のオブジェクト識別子 (OID) のセット要求を発行する NDIS プロトコル ドライバー\_受信\_フィルター\_FREE\_受信キューを解放するキュー。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_キュー\_FREE\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567201)の種類のキュー id を使用した構造**NDIS\_受信\_キュー\_ID**します。

<a name="remarks"></a>注釈
-------

OID の OID の要求を設定する\_受信\_フィルター\_FREE\_キューは NDIS 6.20 が動作し、それ以降のミニポート ドライバーの省略可能です。 仮想マシン キューのインターフェイスをサポートするミニポート ドライバーに対して必要があります。

上位のドライバーの問題の後、 [OID\_受信\_フィルター\_割り当て\_キュー](oid-receive-filter-allocate-queue.md) OID に割り当てる受信キューでは、OID 発行\_受信\_フィルター\_FREE\_受信キューを解放するためのキューの OID。

NDIS ミニポート ドライバー、VMQ を解放するための要求の受信キューに、次の手順に従います。

1.  ネットワーク アダプターには、キューを DMA 停止状態を入力する必要があります、受信キューに関連付けられている受信バッファーへのデータの DMA 転送が停止します。 ネットワーク アダプターは、受信したときにおそらく DMA アクティビティを停止、 [OID\_受信\_フィルター\_オフ\_フィルター](oid-receive-filter-clear-filter.md) OID 要求を受信側の最後のフィルターの設定をクリアするにはキューです。

2.  ミニポート ドライバーが生成されます、 [ **NDIS\_状態\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567417)状態を示す値を**QueueState**のメンバー、 [ **NDIS\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567214)構造体を設定**NdisReceiveQueueOperationalStateDmaStopped** NDIS DMA 転送が停止していることを通知します。

3.  ミニポート ドライバーは、指定された受信パケット、ミニポート ドライバーに返されるキューのすべての待機します。

4.  ミニポート ドライバーのネットワーク アダプターの受信を呼び出して、キューに関連付けられているバッファーが割り当てられているすべての共有メモリを解放する[ **NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)します。

5.  ミニポート ドライバーには、OID が完了すると\_受信\_フィルター\_FREE\_キュー OID 要求を受信キューを解放します。

ミニポート ドライバーの呼び出し、 [ **NdisFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562601)キュー用の共有メモリを解放します。 ドライバーが OID のコンテキストで共有メモリを解放する場合は、ミニポート ドライバーでは、既定以外のキューの共有メモリを割り当て、\_受信\_フィルター\_FREE\_キュー OID 中、キューが解放することができます。 無料のミニポート ドライバーのコンテキストで、既定のキューに割り当てられるメモリの共有、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。

上にある、ドライバーは、設定されると、キューを解放する前に、キューのすべてのフィルターを解放する必要があります。 また、上にある、ドライバーを呼び出す前に、ネットワーク アダプターに割り当てられた、すべての受信キューを解放する必要があります、 [ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)ネットワーク アダプターへのバインドを閉じます。 NDIS ミニポート ドライバーを呼び出す前に、ネットワーク アダプターに割り当てられているすべてのキューの解放[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>関数。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求の次のステータス コードのいずれかを返します。

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
<td><p>完了待ちになっています。 NDIS は最終的な状態コードと結果を渡します OID 要求の完了ハンドラーの呼び出し元の要求が完了した後。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>キューの id が無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS セット、<strong>データ</strong>.<strong>METHOD_INFORMATION</strong>.<strong>BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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


[*MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_キュー\_FREE\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567201)

[**NDIS\_状態\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567417)

[**NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)

[**NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)

[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)

 

 




