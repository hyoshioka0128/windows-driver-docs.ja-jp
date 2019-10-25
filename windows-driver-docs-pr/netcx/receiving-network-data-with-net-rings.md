---
title: ネットリングを使用したネットワークデータの受信
description: このトピックでは、NetAdapterCx クライアントドライバーがネットワークデータを受信するために、ネットリングと net リング反復子を使用する方法について説明します。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx Net リングと net ring 反復子、NetCx Net リングと net ring 反復子、NetAdapterCx PCI devices net ring、NetAdapterCx 非同期 i/o
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3c25e65e5f8db55661071a07eec3de9e54c2b87a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838276"
---
# <a name="receiving-network-data-with-net-rings"></a>ネットワークリングを使用したネットワークデータの受信

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアントドライバーは、フレームワークが受信キューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数を呼び出すと、ネットワークデータを受信します。 このコールバック中に、クライアントドライバーは受信したフラグメントとパケットを OS にドレインし、新しいバッファーをハードウェアにポストすることによって受信を示します。

## <a name="receive-rx-post-and-drain-operation-overview"></a>受信 (Rx) の post とドレイン操作の概要

次のアニメーションは、単純な PCI ネットワークインターフェイスカード (NIC) のクライアントドライバーが受信 (Rx) キューの post 操作とドレイン操作を実行する方法を示しています。 この例のシナリオでは、フラグメントバッファーが割り当てられ、OS によってフラグメントリングにアタッチされます。 この例では、ハードウェア受信キューと OS 受信キューの間に一対一の関係があることを前提としています。

![受信用の Net ring の post およびドレイン操作 (Rx)](images/net_ring_post_and_drain_operations_rx.gif "受信用の Net ring の post およびドレイン操作 (Rx)")

このアニメーションでは、クライアントドライバーが所有するパケットが薄い青と濃い青で強調表示され、クライアントドライバーによって所有されているフラグメントが黄色とオレンジで強調表示されます。 薄い色は、ドライバーが所有する要素の*ドレイン*サブセクションを表します。濃い色は、ドライバーが所有する要素の*post*サブセクションを表します。

## <a name="receiving-data-in-order"></a>受信 (データを順に)

次に示すのは、パケットごとに1つのフラグメントを使用して、データを順番に受信するドライバーの典型的なシーケンスです。

1. **NetRxQueueGetRingCollection**を呼び出して、受信キューのリングコレクション構造を取得します。 これをキューのコンテキスト空間に格納して、ドライバーからの呼び出しを減らすことができます。 
2. ネットワークリングをドレインして OS に受信したデータを示します。
    1. 呼び出しを介して、受信キューのフラグメントリングのドレイン反復子を取得するには、ring[**コレクションを使用します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetdrainfragments)
    2. [**NetRingGetAllPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetallpackets)を呼び出して、パケットリング内の使用可能なすべてのパケットのパケット反復子を取得します。
    3. ループで次の操作を実行します。
        1. フラグメントがハードウェアによって受信されたかどうかを確認します。 それ以外の場合は、ループを中断します。
        2. [**NetFragmentIteratorGetFragment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)を呼び出して、フラグメント反復子の現在のフラグメントを取得します。
        3. 一致するハードウェア記述子に基づいて、そのフラグメントの情報 ( **Validlength**など) を入力します。
        4. [**NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)を呼び出して、このフラグメントのパケットを取得します。
        5. フラグメントをパケットにバインドするには、フラグメントリング内のフラグメントの現在のインデックスにパケットの**Fragmentindex**を設定し、フラグメントの数を適切に設定します (この例では、 **1**に設定します)。 
        6. 必要に応じて、チェックサム情報などの他のパケット情報を入力します。
        7. [**NetFragmentIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratoradvance)を呼び出して次のフラグメントに移動します。
        7. [**NetPacketIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratoradvance)を呼び出して、次のパケットに移動します。
    4. [**NetFragmentIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorset)と[**NetPacketIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorset)を呼び出して、受信したパケットとそのフラグメントを OS に対して確定します。
3. 次に受信するために、ハードウェアにフラグメントバッファーを送信します。    
    1. [**Netringgetpostfragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetpostfragments)を呼び出して、受信キューのフラグメントリングのポスト反復子を取得するには、ring コレクションを使用します。
    2. ループで次の操作を実行します。
        1. [**NetFragmentIteratorGetIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorgetindex)を呼び出して、フラグメント反復子の現在のインデックスを取得します。
        2. フラグメントの情報を一致するハードウェア記述子にポストします。
        3. [**NetFragmentIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratoradvance)を呼び出して次のフラグメントに移動します。
    3. [**NetFragmentIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorset)を呼び出して、ハードウェアへのフラグメントのポストを最終処理します。

これらの手順は、コードで次のようになります。

```cpp
void
MyEvtRxQueueAdvance(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * Rings = rxQueueContext->Rings;

    //
    // Indicate receives by draining the rings
    //
    NET_RING_FRAGMENT_ITERATOR fragmentIterator = NetRingGetDrainFragments(Rings);
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetAllPackets(Rings);
    while(NetFragmentIteratorHasAny(&fragmentIterator))
    {
        UINT32 currentFragmentIndex = NetFragmentIteratorGetIndex(&fragmentIterator);

        // Test for fragment reception
        ...
        //

        NET_FRAGMENT* fragment = NetFragmentIteratorGetFragment(&fragmentIterator);
        fragment->ValidLength = ... ;
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);
        packet->FragmentIndex = currentFragmentIndex;
        packet->FragmentCount = 1;

        if(rxQueueContext->IsChecksumExtensionEnabled)
        {
            // Fill in checksum info
            ...
            //
        }        

        NetFragmentIteratorAdvance(&fragmentIterator);
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetFragmentIteratorSet(&fragmentIterator);
    NetFragmentIteratorSet(&packetIterator);

    //
    // Post fragment buffers to hardware
    //
    fragmentIterator = NetRingGetPostFragments(Rings);
    while(NetFragmentIteratorHasAny(&fragmentIterator))
    {
        UINT32 currentFragmentIndex = NetFragmentIteratorGetIndex(&fragmentIterator);

        // Post fragment information to hardware descriptor
        ...
        //

        NetFragmentIteratorAdvance(&fragmentIterator);
    }
    NetFragmentIteratorSet(&fragmentIterator);
}
```

## <a name="receiving-data-out-of-order"></a>データを順番に受信する

[Tx](sending-network-data-with-net-rings.md)キューとは異なり、クライアントドライバーは、ハードウェア受信キューごとに1つの OS 受信キューがある場合、通常は順序どおりにデータを受信しません。 これは、クライアントドライバーの NIC の種類に関係ありません。 デバイスが PCI ベースであり、OS が受信バッファーを割り当てて所有しているかどうか、またはデバイスが USB ベースであり、USB スタックが受信バッファーを所有しているかどうかは、クライアントドライバーは受信したフラグメントごとにパケットを初期化し、それを OS に示します。 この場合、順序は重要ではありません。

ハードウェアがハードウェア受信キューごとに複数の OS 受信キューをサポートしている場合は、受信バッファーへのアクセスを同期する必要があります。 この作業の範囲は、このトピックの外部にあり、ハードウェアの設計に依存しています。
