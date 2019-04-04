---
title: 要求の送信と受信
description: 要求の送信と受信
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 送信し受信キュー、NetCx 送信および受信キュー
ms.date: 03/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3696a29cbdaf4e4a08b08a7f3ef583c243c0c950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582218"
---
# <a name="transmit-and-receive-queues"></a>要求の送信と受信

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

*パケット キュー*、または*データパス キュー* NetAdapterCx ハードウェアなどのハードウェア機能をモデル化するクライアント ドライバーを有効にするので導入されたオブジェクトの送信し、ソフトウェア ドライバーで、キューをより明示的に受信には. このトピックでは、送信操作および NetAdapterCx でキューを受信する方法について説明します。 

## <a name="creating-transmit-and-receive-queues"></a>送信および受信キューを作成します。

クライアント ドライバーを呼び出すと[ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)、通常はからその[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベントのコールバック関数では、2 つのキューの作成のコールバックを提供します。[*EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)と[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)します。 クライアントは、転送を作成し、これらのコールバックで受信したキューは、それぞれします。

クライアントが呼び出すことによって送信キューを作成するなど、 [ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate)次のようにします。

```C++
NTSTATUS
MyEvtAdapterCreateTxQueue(
    NETADAPTER Adapter, 
    PNETTXQUEUE_INIT NetTxQueueInit
)
{
    NETPACKETQUEUE txQueue;

    // Allocate and initialize the tx queue configuration structure
    NET_PACKET_QUEUE_CONFIG txQueueConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(&txQueueConfig, 
                                 EvtTxQueueAdvance,
                                 EvtTxQueueSetNotificationEnabled,
                                 EvtTxQueueCancel);

    // Optional: set the tx queue's start and stop callbacks
    txQueueConfig.EvtStart = EvtTxQueueStart;
    txQueueConfig.EvtStop = EvtTxQueueStop;

    // Assign fixed size data type as per packet context
    NET_TXQUEUE_CONFIG_SET_DEFAULT_PACKET_CONTEXT_TYPE(&txConfig, MY_CONTEXT);

    // Create the queue
    NTSTATUS status = NetTxQueueCreate(NetTxQueueInit,
                                       WDF_NO_OBJECT_ATTRIBUTES,
                                       &txQueueConfig,
                                       &txQueue);

    return status;
}
```

受信キューを作成する[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)、同じパターンを使用して呼び出す[ **NetRxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuecreate)します。 例については、[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)を参照してください。

フレームワークは、低電力状態に遷移する前にキューを空にし、アダプターを削除する前にそれらを削除します。

## <a name="implementing-queue-callbacks"></a>キューのコールバックを実装します。

送信キュー、または受信キューでは、パケットのキューを作成するときに、クライアントは、次の 3 つのコールバック関数へのポインターを提供する必要があります。

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

さらに、クライアントは、キューの構成構造を初期化した後にこれらのオプションのコールバック関数を指定できます。

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

各イベントのコールバック関数で行う必要があるクライアントは、それぞれの詳細については、これらのページを参照してください。

## <a name="polling-model"></a>ポーリング モデル

NetAdapter データ パスは、ポーリング モデル、および 1 つのパケットのキューでポーリング操作は他のキューの完全に独立しています。 ポーリング モデルは、次の図に示すように、クライアント ドライバーのキューに事前のコールバックを呼び出すことによって実装されます。

![ポーリングのフロー](images/polling.png)

コード例については、[ *EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)を参照してください。

ポーリング操作のシーケンスは次のとおりです。

1. OS は、送信または受信のいずれかのクライアント ドライバーにバッファーを示します。
2. クライアント ドライバーでは、ハードウェアにパケットをプログラムします。
3. クライアント ドライバーでは、OS に完了したパケットを返します。
