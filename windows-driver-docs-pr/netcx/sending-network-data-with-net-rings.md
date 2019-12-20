---
title: ネットリングを使用したネットワークデータの送信
description: このトピックでは、NetAdapterCx クライアントドライバーがネットワークデータを送信するために、ネットリングと net ring 反復子を使用する方法について説明します。
ms.assetid: 2F3DA1A5-D0C1-4928-80B2-AF41F949FF14
keywords:
- NetAdapterCx Net リングと net ring 反復子、NetCx Net リングと net ring 反復子、NetAdapterCx PCI devices net ring、NetAdapterCx 非同期 i/o
ms.date: 11/01/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: 26a2670ba00cb15eff935d5d0892bac05124a465
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208998"
---
# <a name="sending-network-data-with-net-rings"></a>ネット リングを使用したネットワーク データの送信

NetAdapterCx クライアントドライバーは、フレームワークが送信キューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数を呼び出すと、ネットワークデータを送信します。 このコールバック中に、クライアントドライバーは、キューのフラグメントリングからハードウェアにバッファーをポストし、完了したパケットをドレインしてから OS に戻します。

## <a name="transmit-tx-post-and-drain-operation-overview"></a>送信 (Tx) の post とドレイン操作の概要

次のアニメーションは、単純な PCI ネットワークインターフェイスカード (NIC) のクライアントドライバーが送信 (Tx) キューの post 操作とドレイン操作を実行する方法を示しています。  

![送信のための Net ring の post およびドレイン操作 (Tx)](images/net_ring_post_and_drain_operations_tx.gif "送信のための Net ring の post およびドレイン操作 (Tx)")

このアニメーションでは、クライアントドライバーが所有するパケットが薄い青と濃い青で強調表示され、クライアントドライバーによって所有されているフラグメントが黄色とオレンジで強調表示されます。 薄い色は、ドライバーが所有する要素の*ドレイン*サブセクションを表します。濃い色は、ドライバーが所有する要素の*post*サブセクションを表します。

## <a name="sending-data-in-order"></a>送信 (データを順に)

次に示すのは、デバイスがデータを順に転送するドライバー (単純な PCI NIC など) の一般的な post とドレインシーケンスです。

1. [**NetTxQueueGetRingCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuegetringcollection)を呼び出して、送信キューのリングコレクション構造を取得します。 これをキューのコンテキスト空間に格納して、ドライバーからの呼び出しを減らすことができます。 送信キューのパケットリングを取得するには、ring コレクションを使用します。
2. データをハードウェアに投稿する:        
    1. パケットインデックスに UINT32 変数を割り当て、それをパケットリングの**Nextindex**に設定します。これはリングの post サブセクションの始まりです。
    2. ループで次の操作を実行します。
        1. パケットインデックスを使用して[**Netringgetpacketatindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)を呼び出してパケットを取得します。
        2. このパケットを無視するかどうかを確認してください。 無視する場合は、このループの手順6に進みます。 それ以外の場合は、続行します。
        3. このパケットのフラグメントを取得します。 リングコレクションから送信キューのフラグメントリングを取得し、パケットの**Fragmentindex**メンバーからパケットのフラグメントの先頭を取得します。次に、パケットの**fragmentindex**を使用して[**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出して、パケットのフラグメントの末尾を取得します。
        4. ループで次の操作を実行します。
            1. [**Netringgetfragmentatindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)を呼び出して、フラグメントを取得します。
            2. **NET_FRAGMENT**記述子を、関連付けられているハードウェアフラグメント記述子に変換します。
            3. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出して、フラグメントのインデックスを進めます。
        5. フラグメントの反復子の現在の**インデックス**に一致するように、フラグメントリングの**次**のインデックスを更新します。これは、ハードウェアへのポストが完了したことを示します。
        6. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出してパケットインデックスを進めます。
    3. パケットリングの**Nextindex**をパケットインデックスに更新して、ハードウェアへのパケットの送信を完了します。
3. 完了した送信パケットを OS にドレインします:
    1. パケットインデックスをパケットリングの**Beginindex**に設定します。これはリングのドレインサブセクションの始まりです。
    2. ループで次の操作を実行します。
        1. パケットインデックスを使用して[**Netringgetpacketatindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)を呼び出してパケットを取得します。
        2. パケットの送信が完了したかどうかを確認します。 そうでない場合は、ループを中断します。
        3. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出してパケットインデックスを進めます。
    3. パケットリングの**Beginindex**をパケットインデックスに更新して、ハードウェアへのパケットの送信を完了します。

これらの手順は、コードでは次のようになります。 ハードウェア固有の詳細 (ハードウェアに記述子をポストする方法や、正常な post トランザクションをフラッシュする方法など) は、わかりやすくするために残されています。

```cpp
void
MyEvtTxQueueAdvance(
    NETPACKETQUEUE TxQueue
)
{
    //
    // Retrieve the transmit queue's ring collection and packet ring. 
    // This example stores the Tx queue's ring collection in its queue context space.
    //
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * ringCollection = txQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    UINT32 currentPacketIndex = 0;

    //
    // Post data to hardware
    //      
    currentPacketIndex = packetRing->NextIndex;
    while(currentPacketIndex != packetRing->EndIndex)
    {
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);        
        if(!packet->Ignore)
        {
            NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
            UINT32 currentFragmentIndex = packet->FragmentIndex;
            UINT32 fragmentEndIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex + packet->FragmentCount - 1);
            
            for(txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors = 0; 
                currentFragmentIndex != fragmentEndIndex; 
                txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors++)
            {
                NET_FRAGMENT * fragment = NetRingGetFragmentAtIndex(fragmentRing, currentFragmentIndex);

                // Post fragment descriptor to hardware
                ...
                //

                currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
            }

            //
            // Update the fragment ring's Next index to indicate that posting is complete and prepare for draining
            //
            fragmentRing->NextIndex = currentFragmentIndex;
        }
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    packetRing->NextIndex = currentPacketIndex;

    //
    // Drain packets if completed
    //
    currentPacketIndex = packetRing->BeginIndex;
    while(currentPacketIndex != packetRing->NextIndex)
    {        
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex); 
        
        // Test packet for transmit completion by checking hardware ownership flags in the packet's last fragment
        // Break if transmit is not complete
        ...
        //
        
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    packetRing->BeginIndex = currentPacketIndex;
}
```

## <a name="sending-data-out-of-order"></a>データを順不同で送信する

デバイスが順不同で転送を完了する可能性のあるドライバーの場合、インオーダーデバイスとの主な違いは、送信バッファーを割り当てるユーザーと、ドライバーが送信完了のテストを処理する方法です。 DMA 対応の PCI NIC を使用したインオーダー転送の場合、OS は通常、フラグメントバッファーを割り当て、アタッチし、最終的に所有します。 次に、クライアントドライバーは、 *Evtpacketqueueadvance*中に、各フラグメントの対応するハードウェア所有権フラグをテストできます。

このモデルとは対照的に、一般的な USB ベースの NIC について考えてみましょう。 この場合、USB スタックは転送用のメモリバッファーを所有しており、これらのバッファーはシステムメモリ内の他の場所に配置される可能性があります。 USB スタックは、クライアントドライバーが順番どおりに完了していることを示します。そのため、クライアントドライバーは、完了コールバックルーチンの間に、パケットの完了ステータスを個別に記録する必要があります。 そのためには、クライアントドライバーはパケットの**スクラッチ**フィールドを使用するか、キューのコンテキスト空間に情報を格納するなどの他の方法を使用できます。 次に、 [*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)の呼び出しで、クライアントドライバーがこの情報をチェックしてパケット完了テストを行います。 
