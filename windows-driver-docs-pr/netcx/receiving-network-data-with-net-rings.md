---
title: Net リングを使用したネットワーク データの受信
description: このトピックでは、ネットワーク データを受信する、NetAdapterCx クライアント ドライバーが純リングと net リングを行う反復子を使用する方法について説明します。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx Net リングと net リングを行う反復子、NetCx Net リング、net のリングの反復子 NetAdapterCx PCI デバイス net リング、NetAdapterCx 非同期 I/O
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4d01bdddbbf40a4ad1e7d1f687160f762a42b10c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905407"
---
# <a name="receiving-network-data-with-net-rings"></a>Net のリングとネットワーク データの受信

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアント ドライバーは、フレームワークを呼び出すときにネットワーク データを受信、 [ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)受信キュー用コールバック関数。 受信をドレインして、このコールバック中にドライバーを示すクライアントを受け取ると、OS へのパケットのフラグメントのハードウェアに新しいバッファーを投稿します。

## <a name="receive-rx-post-and-drain-operation-overview"></a>(Rx) の投稿を受信し、操作の概要のドレイン

次のアニメーションは、単純な PCI ネットワーク インターフェイス カード (NIC) のクライアント ドライバーが post して実行する方法と、受信 (Rx) キューのドレイン操作を示しています。 この例のシナリオでフラグメント バッファーの割り当てや、OS によってフラグメント リングにアタッチします。 この例では、ハードウェアとの間の一対一のリレーションシップの受信キューと OS の受信キュー。

![Net リング post と (Rx) を受信するための操作をドレイン](images/net_ring_post_and_drain_operations_rx.gif "Net リング post と (Rx) を受信するための操作のドレイン")

このアニメーションでは、クライアント ドライバーによって所有されているパケットが薄い青とダークで強調表示青、およびクライアント ドライバーによって所有されているフラグメントは、黄、オレンジ色で強調表示されます。 薄い色の表現、*ドレイン*暗い色を表すときに、ドライバーを所有する要素のサブセクション、*投稿*ドライバーを所有する要素のサブセクションです。

## <a name="receiving-data-in-order"></a>順序でデータの受信

1 パケットあたり 1 つのフラグメントでの順序でデータを受信するドライバーの一般的な流れを次に示します。

1. 呼び出す**NetRxQueueGetRingCollection**受信キューのリングのコレクション構造体を取得します。 これは、ドライバーからの呼び出しを減らすことに、キューのコンテキストの領域に格納できます。 
2. Net のリングをドレインして、OS に受信したデータを指定します。
    1. リングのコレクションを使用して呼び出すことによって、受信キューのフラグメントのリングのドレイン反復子を取得する[ **NetRingGetDrainFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetdrainfragments)します。
    2. 呼び出すことで、パケットのリングで使用可能なすべてのパケットのパケットの反復子を取得[ **NetRingGetAllPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetallpackets)します。
    3. ループでは、次の操作を行います。
        1. フラグメントが、ハードウェアによって受信されたかどうかを確認します。 それ以外の場合は、ループから抜け出します。
        2. フラグメントの反復子の現在のフラグメントを呼び出して取得[ **NetFragmentIteratorGetFragment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)します。
        3. フラグメントの情報などを入力、 **ValidLength**を基に、一致するハードウェア記述子。
        4. このコード例のパケットを呼び出して取得[ **NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)します。
        5. パケットにするには、パケットのフラグメントをバインド**FragmentIndex**フラグメントの現在のインデックス フラグメント リングし、フラグメントの数を適切に設定する (この例に設定されて**1**). 
        6. 必要に応じて、チェックサム情報など、他のパケット情報を入力します。
        7. 呼び出す[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)を次のフラグメントに移動します。
        7. 呼び出す[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)次のパケットに移動します。
    4. 呼び出す[ **NetFragmentIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorset)と[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset)を示す受信パケットのフラグメントを最終処理OS。
3. 次のハードウェアに post フラグメントのバッファーを受け取ります。    
    1. リングのコレクションを使用して、呼び出すことによって、受信キューのフラグメントのリングの投稿の反復子を取得する[ **NetRingGetPostFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetpostfragments)します。
    2. ループでは、次の操作を行います。
        1. フラグメントの反復子の現在のインデックスを呼び出して取得[ **NetFragmentIteratorGetIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetindex)します。
        2. フラグメントの一致するハードウェア記述子情報を投稿します。
        3. 呼び出す[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)を次のフラグメントに移動します。
    3. 呼び出す[ **NetFragmentIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorset)ハードウェアに転記フラグメントを最終処理します。

次の手順をコードで次のようになります。

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

## <a name="receiving-data-out-of-order"></a>誤順序のデータの受信

異なり、 [Tx](sending-network-data-with-net-rings.md)キュー、クライアント ドライバーは誤順序の OS の受信所有しているハードウェアごとのキューの受信キュー データを受信していない通常します。 これは、クライアント ドライバーの NIC の種類に関係なく、します。 またはかどうか、デバイスは、PCI ベースおよび OS を割り当てるし、受信バッファーを所有しているかどうか、デバイスが USB ベース USB スタックは、受信バッファーを所有している、クライアント ドライバーがパケットを受信した各フラグメントを初期化し、OS にことを示します。 順序はここで重要ではありません。

ハードウェアは、ハードウェアの受信キューごとに 1 つ以上の OS 受信キューをサポートする場合は、受信バッファーへのアクセスを同期する必要があります。 実行のスコープはのでこのトピックの外部し、は、ハードウェアの設計に依存します。
