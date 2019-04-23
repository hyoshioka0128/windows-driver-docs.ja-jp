---
title: 要求の送信と受信
description: 要求の送信と受信
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 送信し受信キュー、NetCx 送信および受信キュー
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d8a103df6facbd9d0144902462c744e209d96d43
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903946"
---
# <a name="transmit-and-receive-queues"></a>要求の送信と受信

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="overview"></a>概要

*パケット キュー*、または*データパス キュー* NetAdapterCx ハードウェアなどのハードウェア機能をモデル化するクライアント ドライバーを有効にするので導入されたオブジェクトの送信し、ソフトウェア ドライバーで、キューをより明示的に受信には. このトピックでは、送信操作および NetAdapterCx でキューを受信する方法について説明します。 

クライアント ドライバーを呼び出すと[ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)、通常はからその[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベントのコールバック関数では、2 つのキューの作成のコールバックを提供します。[*EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)と[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)します。 クライアントは、転送を作成し、これらのコールバックで受信したキューは、それぞれします。

フレームワークは、低電力状態に遷移する前にキューを空にし、アダプターを削除する前にそれらを削除します。

## <a name="creating-packet-queues"></a>パケット キューの作成

送信キュー、または受信キューでは、パケットのキューを作成するときに、クライアントは、次の 3 つのコールバック関数へのポインターを提供する必要があります。

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

さらに、クライアントは、キューの構成構造を初期化した後にこれらのオプションのコールバック関数を指定できます。

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

### <a name="creating-a-transmit-queue"></a>送信キューを作成します。

NetAdapterCx 呼び出し[ *EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)の非常に最後に、[電源投入シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)します。 このコールバック中にクライアント ドライバー通常以下に示します。

- 必要に応じて登録を開始し、キューのコールバックを停止します。
- 呼び出す[ **NetTxQueueInitGetQueueId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueueinitgetqueueid)を設定する送信キューの識別子を取得します。
- 呼び出す[ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate)キューを割り当てることです。 
    - 場合[ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate)が失敗した、 *EvtNetAdapterCreateTxQueue*コールバック関数がエラー コードを返す必要があります。
- パケットの拡張機能のオフセットを照会します。

次の例では、コード内の次の手順が検索する方法を示します。 エラー処理コードは、わかりやすくするためには、この例から除外されています。

```C++
NTSTATUS
EvtAdapterCreateTxQueue(
    _In_    NETADAPTER          Adapter,
    _Inout_ NETTXQUEUE_INIT *   TxQueueInit
)
{
    NTSTATUS status = STATUS_SUCCESS;

    // Prepare the configuration structure
    NET_PACKET_QUEUE_CONFIG txConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(
        &txConfig,
        EvtTxQueueAdvance,
        EvtTxQueueSetNotificationEnabled,
        EvtTxQueueCancel);

    // Optional: register the queue's start and stop callbacks
    txConfig.EvtStart = EvtTxQueueStart;
    txConfig.EvtStop = EvtTxQueueStop;

    // Get the queue ID
    const ULONG queueId = NetTxQueueInitGetQueueId(TxQueueInit);

    // Create the transmit queue
    NETPACKETQUEUE txQueue;
    status = NetTxQueueCreate(
        TxQueueInit,
        &txAttributes,
        &txConfig,
        &txQueue);

    // Get the queue context for storing the queue ID and packet extension offset info
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);

    // Store the queue ID in the context
    queueContext->QueueId = queueId;

    // Query checksum packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY extension;
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1);

    NetTxQueueGetExtension(txQueue, &extension, &queueContext->ChecksumExtension);

    // Query Large Send Offload packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_LSO_NAME,
        NET_PACKET_EXTENSION_LSO_VERSION_1);
    
    NetTxQueueGetExtension(txQueue, &extension, &queueContext->LsoExtension);

    return status;
}
```

### <a name="creating-a-receive-queue"></a>受信キューを作成します。

受信キューを作成する[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)、送信キューの呼び出しと同じパターンを使用して[ **NetRxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuecreate). 

次の例では、コードで受信キューを作成する表示方法を示します。 エラー処理コードは、わかりやすくするためには、この例から除外されています。

```c++
NTSTATUS
EvtAdapterCreateRxQueue(
    _In_ NETADAPTER NetAdapter,
    _Inout_ PNETRXQUEUE_INIT RxQueueInit
)
{
    NTSTATUS status = STATUS_SUCCESS;

    // Prepare the configuration structure
    NET_PACKET_QUEUE_CONFIG rxConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(
        &rxConfig,
        EvtRxQueueAdvance,
        EvtRxQueueSetNotificationEnabled,
        EvtRxQueueCancel);

    // Optional: register the queue's start and stop callbacks
    rxConfig.EvtStart = EvtRxQueueStart;
    rxConfig.EvtStop = EvtRxQueueStop;

    // Get the queue ID
    const ULONG queueId = NetRxQueueInitGetQueueId(RxQueueInit);

    // Create the receive queue
    NETPACKETQUEUE rxQueue;
    status = NetRxQueueCreate(
        RxQueueInit,
        &rxAttributes,
        &rxConfig,
        &rxQueue);

    // Get the queue context for storing the queue ID and packet extension offset info
    PMY_RX_QUEUE_CONTEXT queueContext = GetMyRxQueueContext(rxQueue);

    // Store the queue ID in the context
    queueContext->QueueId = queueId;

    // Query the checksum packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY extension;
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1); 
          
    NetRxQueueGetExtension(rxQueue, &extension, &queueContext->ChecksumExtension);

    return status;
}
```

## <a name="polling-model"></a>ポーリング モデル

NetAdapter データ パスは、ポーリング モデル、および 1 つのパケットのキューでポーリング操作は他のキューの完全に独立しています。 ポーリング モデルは、次の図に示すように、クライアント ドライバーのキューに事前のコールバックを呼び出すことによって実装されます。

![ポーリングのフロー](images/polling.png)

## <a name="advancing-packet-queues"></a>先行するパケット キュー

パケット キューでポーリング操作のシーケンスは次のとおりです。

1. OS は、送信または受信のいずれかのクライアント ドライバーにバッファーを示します。
2. クライアント ドライバーでは、ハードウェアにパケットをプログラムします。
3. クライアント ドライバーでは、OS に完了したパケットを返します。

クライアント ドライバーの内で発生するポーリング操作[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数。 クライアント ドライバーでは、各パケット キューのバックアップと呼ばれる、基になるデータ構造で*net リング*が含まれている、またはシステム メモリ内で実際のネットワーク データ バッファーへのリンクします。 中に*EvtPacketQueueAdvance*、クライアント ドライバーは、送信を実行し、正味のリングでの操作を使用して、受信*リングを行う反復子を net*ハードウェアと OS 間データが格納されるバッファーの所有権を転送します。送信または受信します。

Net のリングと net リングを行う反復子の詳細については、次を参照してください。[リングと net リングを行う反復子を Net](net-rings-and-net-ring-iterators.md)します。

実装の例の*EvtPacketQueueAdvance*送信キューでは、次を参照してください。 [net リングでネットワーク データを送信する](sending-network-data-with-net-rings.md)します。 実装の例の*EvtPacketQueueAdvance*受信キューでは、次を参照してください。 [net リングでネットワーク データを受信して](receiving-network-data-with-net-rings.md)します。

## <a name="enabling-and-disabling-packet-queue-notification"></a>有効にして、パケットのキュー通知を無効化

クライアント ドライバーでは、新しいパケットを受信パケット キューの net リングで、NetAdapterCx 呼び出しますクライアント ドライバーの[ *EvtPacketQueueSetNotificationEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)コールバック関数。 このコールバックでクライアント ドライバーをポーリングすることを示します (の*EvtPacketQueueAdvance*または*EvtPacketQueueCancel*) は停止し、クライアント ドライバーは続行されません[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)または[ **NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)します。 通常、PCI デバイスでは、コールバックを使用して送信を有効にするか、Rx の中断します。 割り込みをもう一度無効にし、クライアント ドライバーは呼び出し、割り込みを受信すると、 **NetTxQueueNotifyMoreCompletedPacketsAvailable**または**NetRxQueueNotifyMoreReceivedPacketsAvailable**再度ポーリングを開始するためにフレームワークをトリガーします。

### <a name="enabling-and-disabling-notification-for-a-transmit-queue"></a>有効にして、送信キューの通知を無効化

PCI の NIC の送信キューの通知を有効にする、通常は、送信キューのハードウェア割り込みを有効にするを意味します。 ハードウェアの割り込みが発生したとき、クライアントが呼び出す[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)その DPC から。

同様に、PCI NIC では、キューの通知を無効にするとは、割り込みを無効にすると、キューに関連付けられています。

通常、クライアントは非同期の I/O モデルのあるデバイスの場合、有効な状態を追跡するために内部フラグを使用します。 このフラグと呼び出し、非同期操作が完了したら、完了ハンドラーを確認します[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)設定されている場合。

NetAdapterCx を呼び出す場合*EvtPacketQueueSetNotificationEnabled*で*NotificationEnabled*設定**FALSE**、クライアントが呼び出す必要がありますいない[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable) NetAdapterCx が次では、このコールバック関数を呼び出すまで*NotificationEnabled*設定**TRUE**.

例:

```C++
VOID
MyEvtTxQueueSetNotificationEnabled(
    _In_ NETPACKETQUEUE TxQueue,
    _In_ BOOLEAN NotificationEnabled
)
{
    // Optional: retrieve queue's WDF context
    MY_TX_QUEUE_CONTEXT *txContext = GetTxQueueContext(TxQueue);

    // If NotificationEnabled is TRUE, enable transmit queue's hardware interrupt
    ...
}

VOID
MyEvtTxInterruptDpc(
    _In_ WDFINTERRUPT Interrupt,
    _In_ WDFOBJECT AssociatedObject
    )
{
    MY_INTERRUPT_CONTEXT *interruptContext = GetInterruptContext(Interrupt);

    NetTxQueueNotifyMoreCompletedPacketsAvailable(interruptContext->TxQueue);
}
```

### <a name="enabling-and-disabling-notification-for-a-receive-queue"></a>有効にして、受信キューの通知を無効化

PCI の NIC のキューの通知は送信キューによく似ていますが受信を有効にします。 これは、受信キューのハードウェア割り込みを有効にすると通常意味します。 ハードウェアの割り込みが発生したとき、クライアントが呼び出す[ **NetRxQueueNotifyMoreReceivedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)その DPC から。

次に、例を示します。

```C++
VOID
MyEvtRxQueueSetNotificationEnabled(
    _In_ NETPACKETQUEUE RxQueue,
    _In_ BOOLEAN NotificationEnabled
)
{
    // optional: retrieve queue's WDF Context
    MY_RX_QUEUE_CONTEXT *rxContext = GetRxQueueContext(RxQueue);

    // If NotificationEnabled is TRUE, enable receive queue's hardware interrupt
    ...
}

VOID
MyEvtRxInterruptDpc(
    _In_ WDFINTERRUPT Interrupt,
    _In_ WDFOBJECT AssociatedObject
    )
{
    MY_INTERRUPT_CONTEXT *interruptContext = GetInterruptContext(Interrupt);

    NetRxQueueNotifyMoreReceivedPacketsAvailable(interruptContext->RxQueue);
}
```

USB デバイス、または、ソフトウェアとその他のキューの受信完了メカニズムは、キューの通知が有効になっているかどうか、クライアント ドライバーが独自のコンテキストで追跡する必要があります。 (、メッセージが、USB の継続的なリーダーで使用できるようになるときに、たとえばトリガーされます)、完了ルーチンから呼び出して[ **NetRxQueueNotifyMoreReceivedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)通知された場合有効になります。 次の例では、これ行う方法を示します。

```C++
VOID
UsbEvtReaderCompletionRoutine(
    _In_ WDFUSBPIPE Pipe,
    _In_ WDFMEMORY Buffer,
    _In_ size_t NumBytesTransferred,
    _In_ WDFCONTEXT Context
)
{
    UNREFERENCED_PARAMETER(Pipe);

    PUSB_RCB_POOL pRcbPool = *((PUSB_RCB_POOL*) Context);
    PUSB_RCB pRcb = (PUSB_RCB) WdfMemoryGetBuffer(Buffer, NULL);

    pRcb->DataOffsetCurrent = 0;
    pRcb->DataWdfMemory = Buffer;
    pRcb->DataValidSize = NumBytesTransferred;

    WdfObjectReference(pRcb->DataWdfMemory);

    ExInterlockedInsertTailList(&pRcbPool->ListHead,
                                &pRcb->Link,
                                &pRcbPool->ListSpinLock);

    if (InterlockedExchange(&pRcbPool->NotificationEnabled, FALSE) == TRUE)
    {
        NetRxQueueNotifyMoreReceivedPacketsAvailable(pRcbPool->RxQueue);
    }
}
```

## <a name="canceling-packet-queues"></a>パケット キューのキャンセル

呼び出して、クライアント ドライバーの開始、OS では、データ パスが停止したら、 [ *EvtPacketQueueCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)コールバック関数。 このコールバックは、クライアント ドライバーが、フレームワークは、パケットのキューを削除する前に必要な処理を実行します。 送信キューのキャンセルは省略可能で、ハードウェアで実行中の送信のキャンセルをサポートするかどうかによって異なりますが、受信キューのキャンセルが必要です。 

中に*EvtPacketQueueCancel*ドライバーでは、net リングを行う反復子を使用して、必要に応じて、OS にパケットを返します。 送信のコード例では、キューおよびキューのキャンセルの受信を参照してください。 [net リングとネットワーク データをキャンセル](canceling-network-data-with-net-rings.md)します。

ドライバーの呼び出し後*EvtPacketQueueCancel*コールバック、フレームワークが、ドライバーのポーリングを継続[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)までのすべてのパケットのコールバックとOS には、バッファーが返されました。
