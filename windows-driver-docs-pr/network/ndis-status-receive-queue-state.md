---
title: NDIS_STATUS_RECEIVE_QUEUE_STATE
description: NDIS_STATUS_RECEIVE_QUEUE_STATE 状態は、キューが変更された仮想マシン キュー (VMQ) のキューの状態が表示されるドライバーに関連するを示します。
ms.assetid: 59b42de9-6aa5-445e-a39a-de2421c945ea
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_QUEUE_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 339a3b978c3ae8f1dfe718e64f0d1a7d7ab6bc69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385077"
---
# <a name="ndisstatusreceivequeuestate"></a>NDIS\_状態\_受信\_キュー\_状態


NDIS\_状態\_受信\_キュー\_キューが変更された仮想マシン キュー (VMQ) のキューの状態が表示されるドライバーに関連する状態のステータスを示します。

<a name="remarks"></a>注釈
-------

NDIS 6.20 が動作し、仮想マシン キューのインターフェイスをサポートする以降のミニポート ドライバーは、この状態を示す値を生成します。

ミニポート ドライバーに用意されている、 [ **NDIS\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)構造体、 **StatusBuffer**のメンバー、[ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。

変更、 *DMA 停止*状態が必要な唯一のキューの状態変更目印です。 受信した後、ミニポート ドライバーはこの状態を示す必要があります、 [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)セットの要求と、DMA が停止します。 この場合、ミニポート ドライバーの設定、 **QueueState**のメンバー、 [ **NDIS\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)構造体**NdisReceiveQueueOperationalStateDmaStopped**します。

ドライバーの受信後、ミニポート、 [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)設定要求と、指定したキューに割り当てられていたすべての共有メモリに DMA を停止する必要があります。

ミニポート ドライバーが何らかの理由により、DMA を停止するかどうか (たとえば、その解放キューの最後のフィルターの場合)、キューを入力する必要があります、 *DMA 停止*状態。 ただしで DMA を停止できます、*一時停止*または*を実行している*状態フィルターがない場合は、キューに設定します。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

 

 




