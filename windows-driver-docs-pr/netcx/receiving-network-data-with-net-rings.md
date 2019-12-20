---
title: ネットリングを使用したネットワークデータの受信
description: このトピックでは、NetAdapterCx クライアントドライバーがネットワークデータを受信するために、ネットリングと net リング反復子を使用する方法について説明します。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx Net リングと net ring 反復子、NetCx Net リングと net ring 反復子、NetAdapterCx PCI devices net ring、NetAdapterCx 非同期 i/o
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: 79b4505d971705f5681ab2db8519bfd049056501
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209002"
---
# <a name="receiving-network-data-with-net-rings"></a>ネット リングを使用したネットワーク データの受信

NetAdapterCx クライアントドライバーは、フレームワークが受信キューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数を呼び出すと、ネットワークデータを受信します。 このコールバック中に、クライアントドライバーは受信したフラグメントとパケットを OS にドレインし、新しいバッファーをハードウェアにポストすることによって受信を示します。

## <a name="receive-rx-post-and-drain-operation-overview"></a>受信 (Rx) の post とドレイン操作の概要

次のアニメーションは、単純な PCI ネットワークインターフェイスカード (NIC) のクライアントドライバーが受信 (Rx) キューの post 操作とドレイン操作を実行する方法を示しています。 この例のシナリオでは、フラグメントバッファーが割り当てられ、OS によってフラグメントリングにアタッチされます。 この例では、ハードウェア受信キューと OS 受信キューの間に一対一の関係があることを前提としています。

![受信用の Net ring の post およびドレイン操作 (Rx)](images/net_ring_post_and_drain_operations_rx.gif "受信用の Net ring の post およびドレイン操作 (Rx)")

このアニメーションでは、クライアントドライバーが所有するパケットが薄い青と濃い青で強調表示され、クライアントドライバーによって所有されているフラグメントが黄色とオレンジで強調表示されます。 薄い色は、ドライバーが所有する要素の*ドレイン*サブセクションを表します。濃い色は、ドライバーが所有する要素の*post*サブセクションを表します。

## <a name="receiving-data-in-order"></a>受信 (データを順に)

次に示すのは、パケットごとに1つのフラグメントを使用して、データを順番に受信するドライバーの典型的なシーケンスです。

1. [**NetRxQueueGetRingCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuegetringcollection)を呼び出して、受信キューのリングコレクション構造を取得します。 これをキューのコンテキスト空間に格納して、ドライバーからの呼び出しを減らすことができます。 受信キューのフラグメントリングとパケットリングのドレイン反復子を取得するには、リングコレクションを使用します。
2. ネットワークリングをドレインして OS に受信したデータを示します。
    1. フラグメントリングの現在のインデックスとパケットリングの現在のインデックスを追跡するために、UINT32 変数を割り当てます。 これらの変数は、リングのドレインサブセクションの先頭であるそれぞれのネットリングの**Beginindex**に設定します。 フラグメントリングの [ドレイン] セクションの末尾に UINT32 変数を割り当てます。これを行うには、フラグメントリングの**Nextindex**に設定します。
    2. ループで次の操作を実行します。
        1. フラグメントがハードウェアによって受信されたかどうかを確認します。 それ以外の場合は、ループを中断します。
        2. [**Netringgetfragmentatindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)を呼び出して、フラグメントを取得します。
        3. 一致するハードウェア記述子に基づいて、そのフラグメントの情報 ( **Validlength**など) を入力します。
        4. [**Netringgetpacketatindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)を呼び出して、このフラグメントのパケットを取得します。
        5. フラグメントをパケットにバインドするには、フラグメントリング内のフラグメントの現在のインデックスにパケットの**Fragmentindex**を設定し、フラグメントの数を適切に設定します (この例では、 **1**に設定します)。 
        6. 必要に応じて、チェックサム情報などの他のパケット情報を入力します。
        7. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出して、フラグメントのインデックスを進めます。
        7. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出してパケットインデックスを進めます。
    3. フラグメントリングの**Beginindex**を現在のフラグメントインデックス変数に更新し、パケットリングの**beginindex**を現在のパケットインデックスに更新して、受信したパケットとそのフラグメントを OS に示すことを確定します。
3. 次に受信するために、ハードウェアにフラグメントバッファーを送信します。    
    1. 現在のフラグメントインデックスを、リングの post サブセクションの先頭であるフラグメントリングの**Nextindex**に設定します。 フラグメントの終了インデックスをフラグメントリングの**EndIndex**に設定します。
    2. ループで次の操作を実行します。
        1. フラグメントの情報を一致するハードウェア記述子にポストします。
        2. [**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)を呼び出して、フラグメントのインデックスを進めます。
    3. フラグメントリングの**Nextindex**を現在のフラグメントインデックス変数に更新して、ハードウェアへのフラグメントのポストを最終処理します。

これらの手順は、コードで次のようになります。

```cpp
void
MyEvtRxQueueAdvance(
    NETPACKETQUEUE RxQueue
)
{
    //
    // Retrieve the receive queue's ring collection and net rings. 
    // This example stores the Rx queue's ring collection in its queue context space.
    //
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * ringCollection = rxQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
    UINT32 currentPacketIndex = 0;
    UINT32 currentFragmentIndex = 0;
    UINT32 fragmentEndIndex = 0;

    //
    // Indicate receives by draining the rings
    //
    currentPacketIndex = packetRing->BeginIndex;
    currentFragmentIndex = fragmentRing->BeginIndex;
    fragmentEndIndex = fragmentRing->NextIndex;
    while(currentFragmentIndex != fragmentEndIndex)
    {
        // Test for fragment reception. Break if fragment has not been received.
        ...
        //

        NET_FRAGMENT * fragment = NetRingGetFragmentAtIndex(fragmentRing, currentFragmentIndex);
        fragment->ValidLength = ... ;
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->FragmentIndex = currentFragmentIndex;
        packet->FragmentCount = 1;

        if(rxQueueContext->IsChecksumExtensionEnabled)
        {
            // Fill in checksum info
            ...
            //
        }        

        currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    fragmentRing->BeginIndex = currentFragmentIndex;
    packetRing->BeginIndex = currentPacketIndex;

    //
    // Post fragment buffers to hardware
    //
    currentFragmentIndex = fragmentRing->NextIndex;
    fragmentEndIndex = fragmentRing->EndIndex;
    while(currentFragmentIndex != fragmentEndIndex)
    {
        // Post fragment information to hardware descriptor
        ...
        //

        currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
    }
    fragmentRing->NextIndex = currentFragmentIndex;
}
```

## <a name="receiving-data-out-of-order"></a>データを順番に受信する

[Tx](sending-network-data-with-net-rings.md)キューとは異なり、クライアントドライバーは、ハードウェア受信キューごとに1つの OS 受信キューがある場合、通常は順序どおりにデータを受信しません。 これは、クライアントドライバーの NIC の種類に関係ありません。 デバイスが PCI ベースであり、OS が受信バッファーを割り当てて所有しているかどうか、またはデバイスが USB ベースであり、USB スタックが受信バッファーを所有しているかどうかは、クライアントドライバーは受信したフラグメントごとにパケットを初期化し、それを OS に示します。 この場合、順序は重要ではありません。

ハードウェアがハードウェア受信キューごとに複数の OS 受信キューをサポートしている場合は、受信バッファーへのアクセスを同期する必要があります。 この作業の範囲は、このトピックの外部にあり、ハードウェアの設計に依存しています。
