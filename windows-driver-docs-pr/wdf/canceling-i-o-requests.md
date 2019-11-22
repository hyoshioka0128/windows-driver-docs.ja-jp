---
title: I/O 要求のキャンセル
description: I/O 要求のキャンセル
ms.assetid: 9a486fa4-7fd3-4433-88aa-34a54d9b1e16
keywords:
- WDK KMDF の要求の処理、要求の取り消し
- I/o 要求 WDK KMDF、取り消し
- i/o 要求のキャンセル (WDK KMDF)
- 未配信 i/o 要求の WDK KMDF
- i/o 要求の転送 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4c6b93b86a441e94b671df3c980851d95f3b529
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844612"
---
# <a name="canceling-io-requests"></a>I/O 要求のキャンセル





デバイスの進行中の i/o 操作 (ディスクからの複数のブロックの読み取り要求など) は、アプリケーション、システム、またはドライバーによって取り消されることがあります。 デバイスの i/o 操作が取り消された場合、i/o マネージャーは i/o 操作に関連付けられているすべての未処理 i/o 要求をキャンセルしようとします。 I/o マネージャーが i/o 要求をキャンセルしようとしたときに、デバイスのドライバーが通知を受け取るように登録することができます。また、ドライバーは、\_状態が [キャンセル] の完了状態を[完了](completing-i-o-requests.md)して、所有している要求をキャンセルできます。

フレームワークは、フレームワークベースのドライバーのキャンセル作業の一部を処理します。 デバイスの i/o 操作が取り消された場合、フレームワークは、取り消された操作に関連付けられている次の i/o 要求 (状態\_canceled の完了状態) を完了します。

-   フレームワークがドライバーの既定の i/o キューに配置した、配信されていない i/o 要求。

-   ドライバーが[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出したため、フレームワークが別のキューに転送した、配信されていない i/o 要求。

これらの要求は、フレームワークによってキャンセルされるため、ドライバーには配信されません。

フレームワークがドライバーに i/o 要求を送信した後、ドライバーは要求を[所有](request-ownership.md)しており、フレームワークはその要求を取り消すことができません。 この時点では、ドライバーのみが i/o 要求をキャンセルできますが、フレームワークは、要求をキャンセルする必要があることをドライバーに通知する必要があります。 ドライバーは、 [*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を提供することによって、この通知を受信します。

場合によっては、ドライバーは i/o キューから i/o 要求を受信しますが、要求を処理するのではなく、ドライバーは要求を同じまたは別の i/o キューにキューして、後で処理することができます。 このような状況の例を次に示します。

-   フレームワークは、ドライバーのいずれかの[要求ハンドラー](request-handlers.md)に i/o 要求を配信し、その後、ドライバーは[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) (または[**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)) を呼び出して、要求を別のに配置します。queue または[**WdfRequestRequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestrequeue)を実行して、要求を同じキューに戻します。

-   フレームワークは、ドライバーの[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数に i/o 要求を配信し、ドライバーは[**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出して要求をフレームワークに戻します。その後、フレームワークは、要求をいずれかのドライバーの i/o キュー。

このような場合は、要求が i/o キューにあるため、フレームワークは i/o 要求を取り消すことができます。 ただし、ドライバーが要求が存在する i/o キューの[*EvtIoCanceledOnQueue*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)コールバック関数を登録している場合、フレームワークは、関連付けられている i/o 操作が実行されているときに、要求をキャンセルするのではなく、コールバック関数を呼び出します。canceled. フレームワークがドライバーの*EvtIoCanceledOnQueue*コールバック関数を呼び出す場合、ドライバーは要求を[完了](completing-i-o-requests.md)する必要があります。

要約すると、i/o 操作が取り消された場合、フレームワークは、ドライバーにまだ配信されていないすべての関連付けられた i/o 要求を常にキャンセルします。 ドライバーが要求を受信してキューすると、ドライバーが i/o キューの[*EvtIoCanceledOnQueue*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)コールバック関数を提供しない限り、フレームワークは要求をキャンセルします (要求がキューにある場合)。

### <a name="calling-wdfrequestmarkcancelable-or-wdfrequestmarkcancelableex"></a>WdfRequestMarkCancelable 可能または WdfRequestMarkCancelableEx を呼び出しています

ドライバーは、 [**Wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出して、 [*evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を登録できます。 ドライバーが**wdfrequestmarkcancelable**または**Wdfrequestmarkcancelableex**を呼び出していて、要求に関連付けられている i/o 操作が取り消された場合、フレームワークはドライバーの*evtrequestcancel*コールバック関数を呼び出して、ドライバーは、i/o 要求を取り消すことができます。

ドライバーは、比較的長い時間の要求を所有する場合は、 [**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出す必要があります。 たとえば、ドライバーは、デバイスが応答するのを待機する必要がある場合や、ドライバーが1つの要求を受信したときに作成された要求のセットをドライバーが完了するまで待機する場合があります。

ドライバーが[**Wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出さない場合、または、 **wdfrequestmarkcancelable**可能または**wdfrequestmarkcancelableex**を呼び出した後に、ドライバーが[**wdfrequestunmarkmarkを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)呼び出した場合ドライバーはキャンセルを認識しないため、通常どおり要求を処理します。

### <a name="calling-wdfrequestiscanceled"></a>WdfRequestIsCanceled を呼び出しています

ドライバーが[**Wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出して[*evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を登録していない場合は、 [**wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出して、i/o マネージャーがi/o 要求をキャンセルします。 **Wdfrequestiscanceled**が**TRUE**を返し、ドライバーが要求を所有している場合、ドライバーは要求をキャンセルする必要があります。 ドライバーが要求を所有していない場合、 **Wdfrequestiscanceled**を呼び出すことはできません。

次の状況では、 [**Wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)という名前のドライバーが[**wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出す可能性があります。

-   デバイスの割り込みを待機するドライバーは、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数から[**Wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出す可能性があります。

-   デバイスをポーリングするドライバーが、it ポーリングスレッドから[**Wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出す可能性があります。

-   [DMA トランザクション](dma-transactions-and-dma-transfers.md)を複数の小さな転送に分割するドライバーは、転送が完了するたびに[**Wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出す可能性があります。

-   大量の読み取り要求または書き込み要求が複数の小さな要求に分割されると、ドライバーが、受信した要求に対して[**Wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出さないと、 [**wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出す可能性があります。

### <a name="canceling-the-request"></a>要求を取り消しています

I/o 要求を取り消すには、次のいずれかが関係している可能性があります。

-   進行中の i/o 操作を停止しています。

-   I/o ターゲットに要求を転送しません。

-   ドライバーが以前に i/o ターゲットに送信した要求をキャンセルしようとしたときに、 [**Wdfrequestcancelの要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)を呼び出しています。

ドライバーがフレームワークから受け取った要求オブジェクトの i/o 要求をキャンセルしている場合、ドライバーは、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[**を呼び出して、常に要求を完了する必要があります。Wdfrequestcompletewith優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)。*状態パラメーターが status\_* が取り消されました。 (要求オブジェクトを作成するために[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)というドライバーが呼び出された場合、ドライバーは要求を完了する代わりに[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出します)。

### <a name="synchronizing-cancellation"></a>取り消しの同期

I/o 要求をキャンセルするコードの同期の詳細については、次を参照してください。

-   [キャンセルと完了コードの同期](synchronizing-cancel-and-completion-code.md)

-   [送信された要求の取り消しの同期](synchronizing-cancellation-of-sent-requests.md)

 

 





