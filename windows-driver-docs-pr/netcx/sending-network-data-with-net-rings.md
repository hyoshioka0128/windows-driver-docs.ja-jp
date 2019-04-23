---
title: Net リングを使用したネットワーク データを送信します。
description: このトピックでは、ネットワーク データを送信する、NetAdapterCx クライアント ドライバーが純リングと net リングを行う反復子を使用する方法について説明します。
ms.assetid: 2F3DA1A5-D0C1-4928-80B2-AF41F949FF14
keywords:
- NetAdapterCx Net リングと net リングを行う反復子、NetCx Net リング、net のリングの反復子 NetAdapterCx PCI デバイス net リング、NetAdapterCx 非同期 I/O
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5c53052e59474ab79bbb7745508d28795a37ca75
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905445"
---
# <a name="sending-network-data-with-net-rings"></a>Net のリングとネットワーク データを送信します。

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアント ドライバーは、フレームワークを呼び出すときに、ネットワーク データを送信、 [ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)送信キューのコールバック関数。 このコールバック中にクライアント ドライバーはハードウェア キューのフラグメントのリングからバッファーを投稿し、完了したパケットと、OS に返すフラグメントのドレインを実行します。

## <a name="transmit-tx-post-and-drain-operation-overview"></a>(テキサス州) の投稿を送信し、操作の概要のドレイン

次のアニメーションは、単純な PCI ネットワーク インターフェイス カード (NIC) のクライアント ドライバーが post して実行する方法と送信 (テキサス州) キューのドレイン操作を示します。  

![Net リング post と送信 (送信) するための操作をドレイン](images/net_ring_post_and_drain_operations_tx.gif "Net リング post と送信 (送信) するための操作をドレイン")

このアニメーションでは、クライアント ドライバーによって所有されているパケットが薄い青とダークで強調表示青、およびクライアント ドライバーによって所有されているフラグメントは、黄、オレンジ色で強調表示されます。 薄い色の表現、*ドレイン*暗い色を表すときに、ドライバーを所有する要素のサブセクション、*投稿*ドライバーを所有する要素のサブセクションです。

## <a name="sending-data-in-order"></a>順序でデータを送信します。

一般的な post とドレインのシーケンスがデバイスなど、単純な PCI NIC の順序でデータを送信するドライバーを次に示します

1. 呼び出す**NetTxQueueGetRingCollection**送信キューのリングのコレクション構造体を取得します。 これは、ドライバーからの呼び出しを減らすことに、キューのコンテキストの領域に格納できます。 
2. ハードウェアに post データ。    
    1. リングのコレクションを使用して呼び出すことによって、送信キューのパケットのリングの投稿の反復子を取得する[ **NetRingGetPostPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetpostpackets)します。
    2. ループでは、次の操作を行います。
        1. パケットを呼び出して取得[ **NetPacketIteratorGetPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)パケット反復子とします。
        2. かどうか、このパケットを無視するかを確認します。 無視する場合は、このループの 6 の手順に進みます。 ない場合は、続行します。
        3. このパケットのフラグメントのフラグメントの反復子を呼び出すことで取得[ **NetPacketIteratorGetFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetfragments)します。
        4. ループ内で次の手順を実行します。
            1. 呼び出す[ **NetFragmentIteratorGetFragment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)のフラグメントを取得するフラグメントの反復子とします。
            2. 変換、 **NET_FRAGMENT**記述子に関連付けられたハードウェア フラグメントの記述子。
            3. 呼び出す[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)このパケットの次のフラグメントに移動します。
        5. 更新プログラムのフラグメントのリングの**次**フラグメントの反復子が一致するインデックスの現在**インデックス**ハードウェアには、その投稿を示しますが、完了します。
        6. 呼び出す[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)次のパケットに移動します。
    3. 呼び出す[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset)ハードウェアに転記パケットを最終処理します。
3. ドレインが完了は、OS にパケットを送信します。
    1. リングのコレクションを使用して、呼び出すことによって、送信キューのパケットのリングのドレイン反復子を取得する[ **NetRingGetDrainPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetdrainpackets)します。
    2. ループでは、次の操作を行います。
        1. パケットを呼び出して取得[ **NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)します。
        2. パケットの送信が完了したかどうかを確認します。 されていない場合は、ループから抜け出します。
        2. 呼び出す[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)次のパケットに移動します。
    3. 呼び出す[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset) OS にドレイン中のパケットを最終処理します。

次の手順をコードで次のようになります。 ハードウェアまたは post が成功したトランザクションをフラッシュする記述子を投稿する方法などのハードウェアに固有の詳細がわかりやすくするために残さことに注意してください。

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

## <a name="sending-data-out-of-order"></a>誤順序のデータの送信

デバイスが順不同の転送を完了可能性がありますドライバーについては、順序でデバイスからプライマリの違いは、送信バッファーを割り当てるユーザーと、ドライバーが、テストの送信完了を処理する方法にあります。 DMA 対応している PCI NIC の順序で上での転送は、OS は通常を割り当てます、アタッチ、最終的にフラグメント バッファーを所有します。 次に、順番にクライアント ドライバーをテストできます各フラグメントの対応するハードウェアの所有権フラグ中に*EvtPacketQueueAdvance*します。

このモデルとは異なり、一般的な USB ベースの NIC を検討してください。 このような状況で USB スタックは、伝送用のメモリ バッファーを所有しているし、これらのバッファーがシステム メモリ内で別の場所にあります。 USB スタックは、クライアント ドライバーは、その完了コールバック ルーチンの中に、個別にパケットの完了ステータスを記録する必要があるために、誤順序のクライアント ドライバーに入力候補を示します。 これを行うには、クライアント ドライバーを使用できます、パケットの**スクラッチ**フィールド、またはそれには、そのキューのコンテキストの領域に情報を格納するように他の方法を使用できます。 次の呼び出しで、 [ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)、クライアント ドライバーがパケットの完了をテストするためには、この情報を確認します。 
