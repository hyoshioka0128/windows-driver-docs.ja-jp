---
title: VM キューの解放
description: VM キューの解放
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51584d5dcfc3cbd0dae85fd49f25ff83c4971e8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842120"
---
# <a name="freeing-a-vm-queue"></a>VM キューの解放





受信キューを解放するために、1つ前のドライバーが Oid を発行して、\_QUEUE set OID 要求を[\_フィルター\_\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_queue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_free_parameters)に対するポインターが含まれています。これには、型のキュー識別子を使用して、無料\_パラメーター構造が含まれます。**NDIS\_\_キュー\_ID を受信**します。

[Oid\_受信\_フィルター\_解放](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)された\_キューは、oid を使用して割り当てられた後のドライバーが\_キュー OID を[割り当てる\_の受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)を使用して割り当てられた受信キューを解放します。 受信キューの割り当ての詳細については、「 [VM キューの割り当て](allocating-a-vm-queue.md)」を参照してください。

**注**  既定のキューは、\_NDIS のキュー識別子を持つ既定のキューであり、 **\_queue\_ID の受信\_既定**のキューが割り当てられており、解放できないことに注意してください。

 

後続のドライバーは、キューを解放する前に、キューに設定されているすべてのフィルターを解放する必要があります。 また、 [**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)関数を呼び出してネットワークアダプターへのバインドを閉じる前に、ネットワークアダプターに割り当てられているすべての受信キューを解放する必要があります。 NDIS は、ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出す前に、ネットワークアダプターに割り当てられているすべてのキューを解放します。

ミニポートドライバーは、キューを解放する要求を受信すると、次のことを行います。

-   は、キューに関連付けられている共有メモリリソースに対して DMA を直ちに停止する必要があります。

-   DMA が停止したことを示すステータスを生成します。

-   キューに関連付けられているすべての未処理の[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体が返されるまで待機します。

-   関連付けられている共有メモリとハードウェアリソースを解放します。

ミニポートドライバーが[\_\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)を使用して\_キューセット要求を取得し\_受信する場合は、キューが停止 dma 状態になる必要があります。キューは、キューの dma を停止し、ミニポートドライバーは、 [**NDIS\_ステータス\_\_キュー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)の状態を示します。 キューの状態の詳細については、「[キューの状態と操作](queue-states-and-operations.md)」を参照してください。

ミニポートドライバーが NDIS\_の状態を発行した後[ **\_\_\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)の状態を示すメッセージが表示されたら、保留中のすべての受信通知が完了するまで待機してから、関連付けられている共有メモリを解放する必要があります。 共有メモリの解放の詳細については、「[共有メモリリソースの割り当て](shared-memory-resource-allocation.md)」を参照してください。

 

 





