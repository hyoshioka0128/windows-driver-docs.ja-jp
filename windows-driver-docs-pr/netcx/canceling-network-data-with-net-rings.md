---
title: Net リングを使用してデータをネットワークのキャンセル
description: このトピックでは、ネットワーク データをキャンセル、NetAdapterCx クライアント ドライバーが純リングと net リングを行う反復子を使用する方法について説明します。
ms.assetid: 009CC1D7-5168-4D7B-9284-04F922D37434
keywords:
- NetAdapterCx Net リング net リングを行う反復子のキャンセル、NetAdapterCx キャンセル パケット キュー
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fc85c6e9a39614c753f33d7a72b760d3294a0fec
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905401"
---
# <a name="canceling-network-data-with-net-rings"></a>Net のリングとネットワーク データのキャンセル

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアント ドライバーは、フレームワークを呼び出すときにネットワークのデータをキャンセル、 [ *EvtPacketQueueCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)パケット キューのコールバック関数。 このコールバックは、クライアント ドライバーが、フレームワークは、パケットのキューを削除する前に必要な処理を実行します。

### <a name="canceling-a-transmit-queue"></a>送信キューのキャンセル

*EvtPacketQueueCancel*コールバック関数の未処理の送信パケットを完了する機会がある送信キューの場合。 異なり、受信キューを使用する必要ありませんこれを行うに。 未処理のパケットの場合、NetAdapterCx を呼び出す、 [ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)送信キューの場合、通常の操作の一部として処理する場所。

キャンセル処理中、ハードウェアのサポートが送信する場合は、過去のすべての取り消されたパケット net リングの post パケットの反復子も進める必要があります。 これは、次の例のようになります可能性があります。

```C++
void
MyEvtTxQueueCancel(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * rings = txQueueContext->Rings;

    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetPostPackets(rings);
    while (NetPacketIteratorHasAny(&packetIterator))
    {
        // Mark this packet as canceled with the scratch field, then move past it
        NetPacketIteratorGetPacket(&packetIterator)->Scratch = 1;
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);
}
```

ハードウェアがキャンセルをサポートしていない場合、このコールバックは、アクションも行わず返すことができます。

### <a name="canceling-a-receive-queue"></a>受信キューのキャンセル

*EvtPacketQueueCancel*コールバック関数の受信キューでは、すべての未処理の受信パケットを行う必要があります。 すべてのパケットを返さない場合は、オペレーティング システムでは、キューは削除されませんし、NetAdapterCx がキューにコールバックを呼び出すことを停止します。 

パケットを返すにする必要がありますが示されている受信パスが無効にされているときに受け取るいずれかを示す最初の試行が無視され、OS にすべてのフラグメントを返すすべてのパケットを設定します。 これは、次のコード例のようになります可能性があります。

> [!NOTE]
> この例は、受信を示すための詳細を残します。 データの受信のコード サンプルは、次を参照してください。 [net リングでネットワーク データを受信して](receiving-network-data-with-net-rings.md)します。

```C++
void
MyEvtRxQueueCancel(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * rings = rxQueueContext->Rings;

    // Set hardware register for cancellation
    ...
    //

    // Indicate receives
    ...
    //

    // Get all packets and mark them for ignoring
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetAllPackets(rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {
        NetPacketIteratorGetPacket(&packetIterator)->Ignore = 1;
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);

    // Return all fragments to the OS
    NET_RING_FRAGMENT_ITERATOR fragmentIterator = NetRingGetAllFragments(rings);
    NetFragmentIteratorAdvanceToTheEnd(&fragmentIterator);
    NetFragmentIteratorSet(&fragmentIterator);
}
```
