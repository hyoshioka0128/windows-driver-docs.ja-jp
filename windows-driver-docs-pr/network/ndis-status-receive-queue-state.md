---
title: NDIS_STATUS_RECEIVE_QUEUE_STATE
description: NDIS_STATUS_RECEIVE_QUEUE_STATE の状態は、仮想マシンキュー (VMQ) の受信キューのキューの状態が変更されたことを示します。
ms.assetid: 59b42de9-6aa5-445e-a39a-de2421c945ea
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_QUEUE_STATE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: b85176044df4fe91fdb37ec2b3aa6fac73f8608d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843519"
---
# <a name="ndis_status_receive_queue_state"></a>NDIS\_ステータス\_\_キュー\_状態を受信します


NDIS\_ステータス\_受信\_キュー\_状態の状態は、仮想マシンキュー (VMQ) の受信キューのキューの状態が変更されたことを示しています。

<a name="remarks"></a>注釈
-------

仮想マシンキューインターフェイスをサポートする NDIS 6.20 以降のミニポートドライバーは、この状態の表示を生成します。

ミニポートドライバーは、ndis [ **\_ステータス\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)れる構造体の**statusbuffer**メンバーで[ **\_キュー\_状態構造体を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)を提供します。

*DMA 停止*状態が変更されるのは、必要なのは、唯一のキュー状態変更であることです。 ミニポートドライバーは、OID を受信した後にこの状態を示す必要があります。 [\_\_フィルターを受信して\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)セット要求を取得し、DMA を停止\_ます。 この場合、ミニポートドライバーは、NDIS の**Queuestate**メンバーを[ **\_受信\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)構造を**NdisReceiveQueueOperationalStateDmaStopped**に設定します。

ミニポートドライバーは、\_フィルターを使用して\_の OID を受信し[\_\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)セット要求を取得した後、指定したキューに割り当てられたすべての共有メモリへの DMA を停止する必要があります。

ミニポートドライバーが他の何らかの理由で DMA を停止した場合 (たとえば、キューの最後のフィルターが解放された場合)、キューは*Dma 停止*状態にならないようにします。 ただし、キューにフィルターが設定されていない場合は、*一時停止*状態または*実行中*の状態で DMA を停止できます。

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
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_RECEIVE\_QUEUE\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_受信\_フィルター\_空き\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

 

 




