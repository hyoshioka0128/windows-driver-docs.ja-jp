---
title: I/O キューの管理
description: I/O キューの管理
ms.assetid: 83cc87c8-7e2d-4f79-a580-0519d327e7ba
keywords:
- I/o キュー WDK KMDF、開始
- I/o キュー WDK KMDF、停止
- I/o キュー WDK KMDF、再起動
- I/o キュー WDK KMDF、要求の追加
- I/o キュー WDK KMDF、要求の取得
- I/o キュー WDK KMDF、要求の検索
- I/o キュー WDK KMDF、削除
- I/o キュー WDK KMDF、ドレイン
- I/o キュー WDK KMDF、移動要求
- I/o キュー WDK KMDF、インターセプト要求
- I/o キュー WDK KMDF、プロパティ
- インターセプト i/o 要求 (WDK KMDF)
- i/o 要求の移行 (WDK KMDF)
- i/o 要求の再配置 WDK KMDF
- i/o 要求の検索 (WDK KMDF)
- キュー i/o 要求 (WDK KMDF)
- i/o キューの停止 WDK KMDF
- i/o キューの再起動 WDK KMDF
- i/o キューの起動 (WDK KMDF)
- メソッドのディスパッチ (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f615f67236b5691246b6183c731b92bd4f4f2f7
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402442"
---
# <a name="managing-io-queues"></a>I/O キューの管理


## <a href="" id="starting-an-i-o-queue"></a>I/o キューを開始しています


ドライバーが[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して i/o キューを作成すると、そのキューが自動的に i/o 要求を受信し、ドライバーに配信されるようになります。

通常、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数内から[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出します。 フレームワークは、ドライバーの*Evtdriverdeviceadd*コールバック関数から制御が戻った後に、ドライバーへの i/o 要求の配信を開始できます。

ドライバーが[電源管理](using-power-managed-i-o-queues.md)の i/o キューを使用している場合、デバイスが動作状態になるまで、フレームワークはドライバーへの要求の配信を開始できず、フレームワークはドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) callback 関数を呼び出します。

## <a href="" id="stopping-and-restarting-an-i-o-queue"></a>I/o キューの停止と再起動


ドライバーは、 [**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)または[**Wdfioqueuestopを同期的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)に呼び出して、フレームワークが i/o キューから i/o 要求を一時的に配信できないようにします。 I/o 要求の配信を再開するために、ドライバーは[**Wdfioqueuestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)を呼び出します。

ドライバーで電源管理の i/o キューが使用されている場合、デバイスが動作 (D0) 状態になると、フレームワークはデバイスのキューを自動的に停止し、デバイスの状態が D0 に戻ったときにフレームワークはキューを再起動します。

## <a href="" id="adding-requests-to-an-i-o-queue"></a>I/o キューへの要求の追加


システムが読み取り、書き込み、またはデバイス i/o 制御要求をドライバーに送信すると、フレームワークは要求を i/o キューに配置します。 ドライバーは、 [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出すことによって、フレームワークが各キューに格納する要求の種類を制御できます。

また、ドライバーは、 [**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出すことによって、フレームワークから受信した要求をキューへすることもできます。

## <a href="" id="obtaining-requests-from-an-i-o-queue"></a>I/o キューから要求を取得する


ドライバーで i/o キューのシーケンシャルまたは並列[ディスパッチ方法](dispatching-methods-for-i-o-requests.md)が指定されている場合、[要求ハンドラー](request-handlers.md)で要求を受信します。

ドライバーが手動またはシーケンシャルなディスパッチ方法を指定する場合、 [**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)または[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)を呼び出すことによって要求を取得できます。

## <a href="" id="searching-for-an-i-o-request"></a>I/o 要求を検索しています


ドライバーで i/o キューの手動[ディスパッチ方法](dispatching-methods-for-i-o-requests.md)が指定されている場合は、次の手順を使用して、キュー内の特定の要求を検索できます。

1.  [**Wdfioqueuefindrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)を呼び出して、ドライバーによって指定された条件に一致する要求を見つけます。

2.  [**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)を呼び出して、 [**Wdfioqueuefindrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)が配置されている要求を取得します。

## <a href="" id="purging-or-draining-an-i-o-queue"></a>I/o キューの消去またはドレイン


I/o キューを*削除*するということは、i/o 要求をキューに挿入したり、キューに既にあるすべての要求を取り消したりすることを意味します。

I/o キューを*ドレイン*することは、キュー内に既にあるすべての要求をドライバーに配信できるようにすると同時に、キューへの i/o 要求の挿入を停止することを意味します。

通常、ドライバーは、キューが電源管理されていない場合にのみ、キューを消去またはドレインします。 電源管理の i/o キューの場合、ドライバーは[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)および[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume) callback 関数を提供できます。

一部のドライバーのキューが電源管理されていない場合は、関連付けられているデバイスまたは i/o チャネルが使用できなくなった場合に、キューの消去またはドレインを行うことができます。 通常は、各要求に非常に重要な情報が含まれている可能性が高い場合を除き、キューを削除するのではなく、削除します。 たとえば、ネットワークデバイスのドライバーによってキューが消去し、記憶装置のドライバーによってキューが消耗する可能性があります。

ドライバーで i/o キューを消去またはドレインする場合、ドライバーは次のいずれかのキューオブジェクトメソッドを呼び出すことができます。

-   [**Wdfioqueuepurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)または[**WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)。 i/o キューへの i/o 要求のキューを停止し、未処理の要求をキャンセルします。

-   [**Wdfioqueuedrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)または[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)を使用すると、既にキューに入っている要求の配信と処理を許可しながら、i/o キューへの i/o 要求を停止できます。

[**Wdfioqueuedrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)と[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)を呼び出すときは注意が必要です。 ドレイン操作は要求の完了を待機するので、キューの保留中の要求が適時に完了することが確実である場合にのみ、キューのドレインを行う必要があります。 I/o 要求の完了にかかる時間がわからず、未処理の要求を取り消すことが許容される場合は、キューを削除することを検討してください。

## <a href="" id="moving-requests-from-one-i-o-queue-to-another"></a>1つの i/o キューから別の i/o キューへの要求の移動


ドライバーが i/o 要求を受け取った後、ドライバーが要求を別の i/o キューにキューへすることが必要になる場合があります。 これを行うには、ドライバーは[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)または[**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)を呼び出します。これにより、指定したキューの末尾に要求が追加されます。 最終的に、フレームワークは、指定されたキューのディスパッチメソッドを使用して、ドライバーに要求を再度配信します。 I/o 要求を1つの i/o キューから別の i/o キューに移動する方法の詳細については、「[キュー I/o requests](requeuing-i-o-requests.md)」を参照してください。

## <a href="" id="intercepting-an-i-o-request-before-it-is-queued"></a>I/o 要求をキューに入れる前にインターセプトする


フレームワークが i/o キューに要求を配置する前に、ドライバーが i/o 要求を受け取ることができます。 I/o 要求をインターセプトするには、ドライバーは[**Wdfdeviceinitsetioincallercontextcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)を呼び出して、 [*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を登録する必要があります。

フレームワークは、 [*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数をデバイスに関連付けます。 その結果、フレームワークは、システムからデバイスに送信される要求を受け取るたびに、 *Evtioincallercontext*コールバック関数を呼び出します。

通常、 [*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数が要求を受け取ると、要求に対していくつかの予備処理が実行されます。 次に、コールバック関数が[**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出します。これにより、要求がフレームワークに返されます。 次に、フレームワークは、要求を適切な i/o キューに配置できます。これは、 *Evtioincallercontext*コールバック関数を呼び出していない場合と同様です。

ドライバーが[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を提供する主な理由は、i/o メソッドをサポートする i/o 操作をドライバーが処理する必要があるということです。これは、[バッファリングも direct i/o でもありませ](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#neither)ん。 この i/o メソッドの場合、ドライバーは i/o 要求の発信元のプロセスコンテキストで受信したバッファーにアクセスする必要があります。 詳細については、「[フレームワークベースのドライバーのデータバッファーへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)」を参照してください。

## <a href="" id="obtaining-i-o-queue-properties"></a>I/o キューのプロパティを取得する


フレームワークキューオブジェクトのプロパティを取得するために、ドライバーは次のメソッドを呼び出すことができます。

-   [**Wdfioqueuegetdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetdevice)。キューオブジェクトが属するデバイスオブジェクトへのハンドルを取得します。

-   [**WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetstate)。キューに関する[状態情報](i-o-queue-states.md)を取得します。

 

 





