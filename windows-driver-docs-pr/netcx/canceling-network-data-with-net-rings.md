---
title: ネットリングを使用したネットワークデータの取り消し
description: このトピックでは、NetAdapterCx クライアントドライバーがネットワークデータをキャンセルするために、ネットリングと net ring 反復子を使用する方法について説明します。
ms.assetid: 009CC1D7-5168-4D7B-9284-04F922D37434
keywords:
- NetAdapterCx Net リングと net ring 反復子のキャンセル、NetAdapterCx cancel packet queue
ms.date: 11/01/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: 7b04db5d637196a9d40387610afe7c0ff1dad785
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210796"
---
# <a name="canceling-network-data-with-net-rings"></a>ネット リングを使用したネットワーク データの取り消し

NetAdapterCx クライアントドライバーは、フレームワークが[*EvtPacketQueueCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)コールバック関数を呼び出してパケットキューを呼び出すときに、ネットワークデータをキャンセルします。 このコールバックは、フレームワークがパケットキューを削除する前に、クライアントドライバーが必要な処理を実行します。

### <a name="canceling-a-transmit-queue"></a>送信キューの取り消し

送信キューの*EvtPacketQueueCancel*コールバック関数では、未処理の送信パケットを完了することができます。 受信キューとは異なり、これを行う必要はありません。 未処理のパケットを残した場合、NetAdapterCx は送信キューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)を呼び出し、通常の操作の一部として処理します。

ハードウェアがフライト中の送信のキャンセルをサポートしている場合は、取り消されたすべてのパケットの後に、ネットリングのパケット反復子を進める必要もあります。 これは、次の例のようになります。

```C++
void
MyEvtTxQueueCancel(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * ringCollection = txQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    UINT32 currentPacketIndex = packetRing->BeginIndex;
    UINT32 packetEndIndex = packetRing->EndIndex;

    while (currentPacketIndex != packetEndIndex)
    {
        // Mark this packet as canceled with the scratch field, then move past it
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->Scratch = 1;
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    
    packetRing->BeginIndex = packetRing->EndIndex;
}
```

ハードウェアがキャンセルをサポートしていない場合、このコールバックはアクションを行わずにを返すことができます。

### <a name="canceling-a-receive-queue"></a>受信キューの取り消し

受信キューの*EvtPacketQueueCancel*コールバック関数では、未処理の受信パケットをすべて完了する必要があります。 すべてのパケットを返さない場合、オペレーティングシステムはキューを削除せず、NetAdapterCx はキューのコールバックの呼び出しを停止します。 

パケットを返すには、まず、受信パスが無効になっているときに指定されている可能性のある受信を指定してから、すべてのパケットを無視し、すべてのフラグメントを OS に返すように設定する必要があります。 これは、次のコード例のようになります。

> [!NOTE]
> この例では、受信を示すの詳細を表示しません。 データを受信するコードサンプルについては、「 [net リングを使用したネットワークデータの受信](receiving-network-data-with-net-rings.md)」を参照してください。

```C++
void
MyEvtRxQueueCancel(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * ringCollection = rxQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
    UINT32 currentPacketIndex = packetRing->BeginIndex;
    UINT32 packetEndIndex = packetRing->EndIndex;

    // Set hardware register for cancellation
    ...
    //

    // Indicate receives
    ...
    //

    // Get all packets and mark them for ignoring
    currentPacketIndex = packetRing->BeginIndex;
    while(currentPacketIndex != packetEndIndex)
    {
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->Ignore = 1;
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    
    packetRing->BeginIndex = packetRing->EndIndex;

    // Return all fragments to the OS
    fragmentRing->BeginIndex = fragmentRing->EndIndex;
}
```
