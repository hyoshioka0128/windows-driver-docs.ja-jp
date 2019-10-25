---
title: ネットリングを使用したネットワークデータの送信
description: このトピックでは、NetAdapterCx クライアントドライバーがネットワークデータを送信するために、ネットリングと net ring 反復子を使用する方法について説明します。
ms.assetid: 2F3DA1A5-D0C1-4928-80B2-AF41F949FF14
keywords:
- NetAdapterCx Net リングと net ring 反復子、NetCx Net リングと net ring 反復子、NetAdapterCx PCI devices net ring、NetAdapterCx 非同期 i/o
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c5a242f5f3c62d5e39141c48e0d8ed14efbd152c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835424"
---
# <a name="sending-network-data-with-net-rings"></a>ネット リングを使用したネットワーク データの送信

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアントドライバーは、フレームワークが送信キューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数を呼び出すと、ネットワークデータを送信します。 このコールバック中に、クライアントドライバーは、キューのフラグメントリングからハードウェアにバッファーをポストし、完了したパケットをドレインしてから OS に戻します。

## <a name="transmit-tx-post-and-drain-operation-overview"></a>送信 (Tx) の post とドレイン操作の概要

次のアニメーションは、単純な PCI ネットワークインターフェイスカード (NIC) のクライアントドライバーが送信 (Tx) キューの post 操作とドレイン操作を実行する方法を示しています。  

![送信のための Net ring の post およびドレイン操作 (Tx)](images/net_ring_post_and_drain_operations_tx.gif "送信のための Net ring の post およびドレイン操作 (Tx)")

このアニメーションでは、クライアントドライバーが所有するパケットが薄い青と濃い青で強調表示され、クライアントドライバーによって所有されているフラグメントが黄色とオレンジで強調表示されます。 薄い色は、ドライバーが所有する要素の*ドレイン*サブセクションを表します。濃い色は、ドライバーが所有する要素の*post*サブセクションを表します。

## <a name="sending-data-in-order"></a>送信 (データを順に)

次に示すのは、デバイスがデータを順に転送するドライバー (単純な PCI NIC など) の一般的な post とドレインシーケンスです。

1. **NetTxQueueGetRingCollection**を呼び出して、送信キューのリングコレクション構造を取得します。 これをキューのコンテキスト空間に格納して、ドライバーからの呼び出しを減らすことができます。 
2. データをハードウェアに投稿する:    
    1. 発信キューのパケットリングのポスト反復子を取得するには、ring コレクションを[**使用します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetpostpackets)。
    2. ループで次の操作を実行します。
        1. パケット反復子を使用して[**NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)を呼び出すことにより、パケットを取得します。
        2. このパケットを無視するかどうかを確認してください。 無視する場合は、このループの手順6に進みます。 それ以外の場合は、続行します。
        3. [**NetPacketIteratorGetFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorgetfragments)を呼び出して、このパケットのフラグメントのフラグメント反復子を取得します。
        4. ループで次の操作を実行します。
            1. フラグメントを取得するには、フラグメント反復子を使用して[**NetFragmentIteratorGetFragment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)を呼び出します。
            2. **NET_FRAGMENT**記述子を、関連付けられているハードウェアフラグメント記述子に変換します。
            3. このパケットの次のフラグメントに移動するには、 [**NetFragmentIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratoradvance)を呼び出します。
        5. フラグメントの反復子の現在の**インデックス**に一致するように、フラグメントリングの**次**のインデックスを更新します。これは、ハードウェアへのポストが完了したことを示します。
        6. [**NetPacketIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratoradvance)を呼び出して、次のパケットに移動します。
    3. [**NetPacketIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorset)を呼び出して、ハードウェアへのパケットの送信を完了します。
3. 完了した送信パケットを OS にドレインします:
    1. 発信キューのパケットリングのドレイン反復子を取得するには、ring コレクションを[**使用します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetdrainpackets)。
    2. ループで次の操作を実行します。
        1. [**NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)を呼び出してパケットを取得します。
        2. パケットの送信が完了したかどうかを確認します。 そうでない場合は、ループを中断します。
        2. [**NetPacketIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratoradvance)を呼び出して、次のパケットに移動します。
    3. [**NetPacketIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorset)を呼び出して、OS へのパケットのドレインを完了します。

これらの手順は、コードでは次のようになります。 ハードウェア固有の詳細 (ハードウェアに記述子をポストする方法や、正常な post トランザクションをフラッシュする方法など) は、わかりやすくするために残されています。

```cpp
void
MyEvtTxQueueAdvance(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * Rings = txQueueContext->Rings;

    //
    // Post data to hardware
    //
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetPostPackets(Rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);        
        if(!packet->Ignore)
        {
            NET_FRAGMENT_ITERATOR fragmentIterator = NetPacketIteratorGetFragments(&packetIterator);
            UINT32 packetIndex = NetPacketIteratorGetIndex(&packetIterator);
            
            for(txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors = 0; 
                NetFragmentIteratorHasAny(&fragmentIterator); 
                txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors++)
            {
                NET_FRAGMENT* fragment = NetFragmentIteratorGetFragment(&fragmentIterator);

                // Post fragment descriptor to hardware
                ...
                //

                NetFragmentIteratorAdvance(&fragmentIterator);
            }

            //
            // Update the fragment ring's Next index to indicate that posting is complete and prepare for draining
            //
            fragmentIterator.Iterator.Rings->Rings[NET_RING_TYPE_FRAGMENT]->NextIndex = NetFragmentIteratorGetIndex(&fragmentIterator);
        }
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);

    //
    // Drain packets if completed
    //
    packetIterator = NetRingGetDrainPackets(Rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {        
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);
        
        // Test packet for transmit completion by checking hardware ownership flags in the packet's last fragment
        ..
        //
        
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);
}
```

## <a name="sending-data-out-of-order"></a>データを順不同で送信する

デバイスが順不同で転送を完了する可能性のあるドライバーの場合、インオーダーデバイスとの主な違いは、送信バッファーを割り当てるユーザーと、ドライバーが送信完了のテストを処理する方法です。 DMA 対応の PCI NIC を使用したインオーダー転送の場合、OS は通常、フラグメントバッファーを割り当て、アタッチし、最終的に所有します。 次に、クライアントドライバーは、 *Evtpacketqueueadvance*中に、各フラグメントの対応するハードウェア所有権フラグをテストできます。

このモデルとは対照的に、一般的な USB ベースの NIC について考えてみましょう。 この場合、USB スタックは転送用のメモリバッファーを所有しており、これらのバッファーはシステムメモリ内の他の場所に配置される可能性があります。 USB スタックは、クライアントドライバーが順番どおりに完了していることを示します。そのため、クライアントドライバーは、完了コールバックルーチンの間に、パケットの完了ステータスを個別に記録する必要があります。 そのためには、クライアントドライバーはパケットの**スクラッチ**フィールドを使用するか、キューのコンテキスト空間に情報を格納するなどの他の方法を使用できます。 次に、 [*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)の呼び出しで、クライアントドライバーがこの情報をチェックしてパケット完了テストを行います。 
