---
title: 要求の送信と受信
description: 要求の送信と受信
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 送受信キュー、NetCx 送受信キュー
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1b3ea0d727923ba62a2ad21db4f52c8a9730fef9
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208964"
---
# <a name="transmit-and-receive-queues"></a>要求の送信と受信

## <a name="overview"></a>概要

*パケットキュー*(*データパス queue* ) は、NetAdapterCx で導入されたオブジェクトです。これにより、クライアントドライバーは、ハードウェアの送信キューや受信キューなどのハードウェア機能をソフトウェアドライバーでより明確にモデル化できるようになります。 このトピックでは、NetAdapterCx で転送キューと受信キューを使用する方法について説明します。 

クライアントドライバーは、通常、 [*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数から[**NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)を呼び出すと、 [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)と[*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)の2つのキュー作成コールバックを提供します。 クライアントは、これらのコールバックにそれぞれ送信キューと受信キューを作成します。

このフレームワークは、低電力状態に移行する前にキューを空にして、アダプターを削除する前にキューを削除します。

## <a name="creating-packet-queues"></a>パケットキューの作成

パケットキュー (送信キューまたは受信キュー) を作成する場合、クライアントは次の3つのコールバック関数へのポインターを提供する必要があります。

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

また、クライアントは、キュー構成構造を初期化した後で、次のオプションのコールバック関数を提供できます。

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

### <a name="creating-a-transmit-queue"></a>送信キューの作成

NetAdapterCx は、[パワーアップシーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)の最後に[*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)を呼び出します。 このコールバック中に、クライアントドライバーは通常、次の操作を実行します。

- 必要に応じて、キューの開始と停止のコールバックを登録します。
- [**Nettxqueueinitgetqueueid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueueinitgetqueueid)を呼び出して、設定する送信キューの識別子を取得します。
- [**NetTxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuecreate)を呼び出してキューを割り当てます。 
    - [**NetTxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuecreate)が失敗した場合、 *EvtNetAdapterCreateTxQueue* callback 関数はエラーコードを返す必要があります。
- パケットの拡張オフセットを照会します。

次の例では、これらの手順がコードでどのように表示されるかを示します。 わかりやすくするために、エラー処理コードはこの例から除外されています。

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
    NET_EXTENSION_QUERY extension;
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1);

    NetTxQueueGetExtension(txQueue, &extension, &queueContext->ChecksumExtension);

    // Query Large Send Offload packet extension offset and store it in the context
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_LSO_NAME,
        NET_PACKET_EXTENSION_LSO_VERSION_1);
    
    NetTxQueueGetExtension(txQueue, &extension, &queueContext->LsoExtension);

    return status;
}
```

### <a name="creating-a-receive-queue"></a>受信キューの作成

[*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)から受信キューを作成するには、送信キューと同じパターンを使用し、 [**NetRxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuecreate)を呼び出します。 

次の例では、受信キューを作成する方法を示します。 わかりやすくするために、エラー処理コードはこの例から除外されています。

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
    NET_EXTENSION_QUERY extension;
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1); 
          
    NetRxQueueGetExtension(rxQueue, &extension, &queueContext->ChecksumExtension);

    return status;
}
```

## <a name="polling-model"></a>ポーリングモデル

NetAdapter データパスはポーリングモデルであり、1つのパケットキューでのポーリング操作は、他のキューから完全に独立しています。 ポーリングモデルは、次の図に示すように、クライアントドライバーのキューのアドバンスコールバックを呼び出すことによって実装されます。

![ポーリングフロー](images/polling.png)

## <a name="advancing-packet-queues"></a>パケットキューを進める

パケットキューでのポーリング操作の順序は次のとおりです。

1. OS は、送信または受信のためにクライアントドライバーにバッファーを提供します。
2. クライアントドライバーは、パケットをハードウェアに対してプログラムします。
3. クライアントドライバーは、完了したパケットを OS に返します。

ポーリング操作は、クライアントドライバーの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック関数内で発生します。 クライアントドライバーの各パケットキューは、ネットワーク*リング*と呼ばれる基になるデータ構造によって支えられています。これには、システムメモリ内の実際のネットワークデータバッファーを格納したり、そのデータをリンクしたりします。 *Evtpacketqueueadvance*の実行中に、クライアントドライバーは、リング内のインデックスを制御し、データの送受信時にハードウェアと OS の間でバッファーの所有権を転送することで、送信と受信の操作を実行します。

ネットワークリングの詳細については、「 [net リングの概要](introduction-to-net-rings.md)」を参照してください。

送信キューに*Evtpacketqueueadvance*を実装する例については、「 [net リングを使用したネットワークデータの送信](sending-network-data-with-net-rings.md)」を参照してください。 受信キューに対して*Evtpacketqueueadvance*を実装する例については、「 [net リングを使用したネットワークデータの受信](receiving-network-data-with-net-rings.md)」を参照してください。

## <a name="enabling-and-disabling-packet-queue-notification"></a>パケットキュー通知の有効化と無効化

クライアントドライバーがパケットキューのネットワークリングで新しいパケットを受信すると、NetAdapterCx はクライアントドライバーの[*Evtpacketqueuesetnotificationenabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)コールバック関数を呼び出します。 このコールバックは、クライアントドライバーがポーリング (of *Evtpacketqueueadvance*または*EvtPacketQueueCancel*) を停止し、クライアントドライバーが[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)または[**NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)を呼び出すまで続行されないことを示します。 通常、PCI デバイスはこのコールバックを使用して、Tx または Rx の割り込みを有効にします。 割り込みが受信されると、割り込みを再び無効にし、クライアントドライバーが**NetTxQueueNotifyMoreCompletedPacketsAvailable**または**NetRxQueueNotifyMoreReceivedPacketsAvailable**を呼び出して、もう一度ポーリングを開始するようにフレームワークをトリガーすることができます。

### <a name="enabling-and-disabling-notification-for-a-transmit-queue"></a>送信キューの通知を有効または無効にする

PCI NIC の場合、送信キュー通知を有効にすることは、通常、送信キューのハードウェア割り込みを有効にすることを意味します。 ハードウェアの割り込みが発生すると、クライアントは DPC から[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)を呼び出します。

同様に、PCI NIC の場合、キュー通知を無効にすると、キューに関連付けられている割り込みが無効になります。

非同期 i/o モデルを持つデバイスの場合、クライアントは通常、内部フラグを使用して有効な状態を追跡します。 非同期操作が完了すると、完了ハンドラーがこのフラグをチェックし、設定されている場合は[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)を呼び出します。

NetAdapterCx が*Notificationenabled*が**FALSE**に設定された*Evtpacketqueuesetnotificationenabled*を呼び出す場合、NetAdapterCx next は*notificationenabled*が**TRUE**に設定されたこのコールバック関数[**を呼び出す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)必要があります。

次に、例を示します。

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

### <a name="enabling-and-disabling-notification-for-a-receive-queue"></a>受信キューの通知を有効または無効にする

PCI NIC の場合、受信キュー通知の有効化は Tx キューと非常によく似ています。 これは通常、受信キューのハードウェア割り込みを有効にすることを意味します。 ハードウェアの割り込みが発生すると、クライアントは DPC から[**NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)を呼び出します。

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

USB デバイス、またはソフトウェアの受信完了メカニズムを持つその他のキューの場合、クライアントドライバーは、キューの通知が有効になっているかどうかを独自のコンテキストで追跡する必要があります。 完了ルーチンから (たとえば、USB 連続リーダーでメッセージが使用可能になったときにトリガーされる)、通知が有効になっている場合は[**NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)を呼び出します。 次の例は、その方法を示しています。

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

## <a name="canceling-packet-queues"></a>パケットキューの取り消し

OS は、データパスを停止すると、クライアントドライバーの[*EvtPacketQueueCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)コールバック関数を呼び出すことによって開始されます。 このコールバックは、フレームワークがパケットキューを削除する前に、クライアントドライバーが必要な処理を実行します。 送信キューのキャンセルはオプションであり、ハードウェアがフライト中の送信のキャンセルをサポートしているかどうかによって異なりますが、受信キューのキャンセルが必要になります。 

*EvtPacketQueueCancel*中に、ドライバーは必要に応じてパケットを OS に返します。 転送キューと受信キューのキャンセルのコード例については、「 [net リングを使用したネットワークデータの取り消し](canceling-network-data-with-net-rings.md)」を参照してください。

ドライバーの*EvtPacketQueueCancel*コールバックを呼び出した後、すべてのパケットとバッファーが OS に返されるまで、フレームワークはドライバーの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバックをポーリングし続けます。
