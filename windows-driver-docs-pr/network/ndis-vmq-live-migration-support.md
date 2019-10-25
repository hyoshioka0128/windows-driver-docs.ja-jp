---
title: NDIS VMQ ライブ マイグレーションのサポート
description: NDIS VMQ ライブ マイグレーションのサポート
ms.assetid: 6872594a-35f8-4fbf-b764-22b286fb940c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08547368d2678998a75cd6060c44d6dfd0c9a021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834643"
---
# <a name="ndis-vmq-live-migration-support"></a>NDIS VMQ ライブ マイグレーションのサポート





ライブマイグレーションをサポートするには、任意の命令または保留中の i/o 境界で仮想マシン (VM) を一時停止することができます。 つまり、VM は保留中の受信要求を完了しない可能性があります。 そのため、ネットワーク仮想サービスプロバイダー (VSP) は、VM から返されなかった、基になるネットワークアダプターに対して受信したすべてのパケットを返します。

**注**  hyper-v では、子パーティションは VM とも呼ばれます。

 

VM が別のホストで再起動されると、新しいホスト上のネットワーク VSP は、再開された VM が返す受信パケットを処理し、ミニポートドライバーの基になる新しいにはそれらを渡しません。 移行が完了すると、その VM に関連付けられている受信キューが解放され、別の VM で再利用できるようになります。

新しいネットワークアダプターで VMQ がサポートされていない可能性がある  に**注意**してください。

 

NDIS は、VMQ 受信キューを解放するようにミニポートドライバーを要求するときに、次の手順を実行します。

1.  ネットワークアダプターは、受信キューに関連付けられているバッファーを受信するために、データの DMA 転送を停止します。その後、キューは DMA 停止状態になる必要があります。 ネットワークアダプターは、Oid を受信したときに DMA アクティビティを停止したことがあります。 [\_受信\_\_フィルターをクリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter) oid 要求を受信して、受信キューの最後の set フィルターをクリアします。

2.  ミニポートドライバーによって、ndis\_の状態[ **\_受信\_\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state)の状態が表示されます。これには、 [**ndis\_receive\_queue\_state**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state) Structure set の**queuestate**メンバーが含まれます。**NdisReceiveQueueOperationalStateDmaStopped**に、DMA 転送が停止されたことを NDIS に通知します。

3.  ミニポートドライバーは、そのキューのすべての受信パケットがミニポートドライバーに返されるまで待機します。

4.  ミニポートドライバーは、 [**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)を呼び出すことによって、キューに関連付けられているネットワークアダプターの受信バッファーに割り当てられたすべての共有メモリを解放します。

5.  ミニポートドライバーは、receive キューを解放するために、 [\_QUEUE oid 要求\_\_フィルターの\_を受信する oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)を完了します。

キューの状態の詳細については、「 [NDIS VM Queue states](ndis-virtual-machine-queue-states.md)」を参照してください。

 

 





