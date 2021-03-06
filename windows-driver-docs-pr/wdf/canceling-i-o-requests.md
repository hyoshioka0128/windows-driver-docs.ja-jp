---
title: I/O 要求のキャンセル
description: I/O 要求のキャンセル
ms.assetid: 9a486fa4-7fd3-4433-88aa-34a54d9b1e16
keywords:
- 要求の WDK KMDF、キャンセル要求を処理します。
- I/O 要求のキャンセルの WDK KMDF
- WDK KMDF を要求する I/O のキャンセル
- 配信されなかった I/O 要求の WDK KMDF
- WDK KMDF を要求する I/O の転送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28bec753047dd8d863d6ade33aca33ba3b7f3a00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377508"
---
# <a name="canceling-io-requests"></a>I/O 要求のキャンセル





アプリケーションやシステム、ドライバーでは、(いくつかのブロックをディスクから読み取る要求) などのデバイスの進行中の I/O 操作をキャンセルできます。 デバイスの I/O 操作が取り消された場合、I/O マネージャーは、I/O 操作に関連付けられているすべての未処理 I/O 要求をキャンセルしようとします。 デバイスのドライバーが I/O マネージャーが、I/O 要求をキャンセルしようとして、ドライバーは、自分が所有する要求をキャンセルできるときに通知を登録できます[完了](completing-i-o-requests.md)ステータスの完了ステータスに\_取り消されました。

フレームワークは、フレームワークに基づいたドライバーの取り消し処理の一部を処理します。 フレームワークには、次の I/O 要求が完了すると、デバイスの I/O 操作が取り消された場合 (状態を表す完了状態で\_CANCELLED) が取り消された操作に関連付けられています。

-   未配信 I/O は、I/O キュー、ドライバーの既定値にフレームワークが格納されたことを要求します。

-   フレームワークは、ドライバーが呼び出されるために、別のキューに転送する I/O 要求を配信できなかった[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)します。

フレームワークは、これらの要求をキャンセルしたため、いないドライバーに配信には。

フレームワークには、ドライバーのドライバーに、I/O 要求が配信された後[所有](request-ownership.md)要求と、フレームワークはこれで取り消すことはできません。 この時点では、ドライバーのみが、I/O 要求をキャンセルできますが、フレームワークは、ドライバーを通知する必要があります、要求を取り消す必要があります。 ドライバーが提供することでこの通知を受信する[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数。

場合があります、ドライバー、I/O キューから I/O 要求を受信するが、要求を処理するのではなく、ドライバー キューに再登録を同じまたは別の要求後で処理するための I/O キュー。 このような状況の例については、次のとおりです。

-   フレームワークのドライバーのいずれかに、I/O 要求を提供する[要求ハンドラー](request-handlers.md)、ドライバーが、その後いずれかを呼び出すと[ **WdfRequestForwardToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) (または[**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)) 要求を別のキューに配置するか、 [ **WdfRequestRequeue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestrequeue)を配置する、同じキューに要求します。

-   フレームワークは、ドライバーに、I/O 要求を配信[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数では、ドライバー呼び出し[ **WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)フレームワークにバックアップ要求を渡すし、その後、フレームワークは、ドライバーの I/O キューのいずれかで要求を配置します。

このような場合は、フレームワークは、要求が、I/O キューであるため、I/O 要求をキャンセルできます。 ただし、ドライバーが登録されている場合、 [ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)要求が存在する I/O キューのコールバック関数、フレームワークの呼び出しをキャンセルではなく、コールバック関数、関連する I/O 操作がキャンセルされた場合に要求します。 フレームワークは、ドライバーの場合*EvtIoCanceledOnQueue*コールバック関数では、ドライバーの必要があります[完了](completing-i-o-requests.md)要求。

要約すると、I/O 操作が取り消されたときに、フレームワークがドライバーに配信されたことはありませんすべての関連する I/O 要求にキャンセルする常にします。 ドライバーが要求を受信し、そのキューに再登録する場合、framework 要求をキャンセルします (要求がキューにある場合)、ドライバーを提供しない限り、 [ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)用コールバック関数I/O キューです。

### <a name="calling-wdfrequestmarkcancelable-or-wdfrequestmarkcancelableex"></a>WdfRequestMarkCancelable または WdfRequestMarkCancelableEx を呼び出す

ドライバーが呼び出せる[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を登録する、 [ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数。 ドライバーが呼び出された場合**WdfRequestMarkCancelable**または**WdfRequestMarkCancelableEx**要求に関連付けられている I/O 操作が取り消された場合、フレームワーク、ドライバーのと*EvtRequestCancel*コールバック関数のため、ドライバーは、I/O 要求を取り消すことができます。

ドライバーを呼び出す必要があります[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)の要求を所有する場合、比較的時間。 たとえば、ドライバーは、デバイスが応答を待機する必要がありますまたは一連のドライバーを作成する要求を完了する下位のドライバーを待つ場合が 1 つの要求を受け取ったとき。

ドライバーが要求されていない場合[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)ドライバーがを呼び出す場合、または[ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)呼び出した後**WdfRequestMarkCancelable**または**WdfRequestMarkCancelableEx**、ドライバーキャンセルを認識しないと、したがって通常どおり要求を処理します。

### <a name="calling-wdfrequestiscanceled"></a>WdfRequestIsCanceled を呼び出す

ドライバーが呼び出されていない場合[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を登録する、 [*EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)呼び出すことができるコールバック関数、 [ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) I/O マネージャーがしようとかどうかを判断するにはI/O 要求をキャンセルします。 場合**WdfRequestIsCanceled**返します**TRUE**ドライバーは、要求を所有しているとは、ドライバーは、要求をキャンセルする必要があります。 呼び出す必要がありますいない場合は、ドライバーが要求を所有していない**WdfRequestIsCanceled**します。

呼び出されていないドライバー [ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)呼び出す[**WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)次の状況で。

-   デバイスの割り込みを呼び出すを待機するドライバー [ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)からその[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数。

-   そのデバイスをポーリングするドライバーを呼び出すことができます[ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)ポーリング スレッドから。

-   分割するドライバー、 [DMA トランザクション](dma-transactions-and-dma-transfers.md)小さいいくつかの転送に呼び出すことができます[ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)各転送の完了後します。

-   受け取る、大規模なドライバーの読み取りまたは書き込み要求をいくつかの小さな要求に分割が呼び出す可能性があります[ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)ドライバーの I/O のターゲットが各小規模の要求が完了したらドライバーが呼び出されていない場合[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)受信用要求。

### <a name="canceling-the-request"></a>要求をキャンセル

I/O 要求をキャンセル、次のいずれかがあります。

-   進行中の I/O 操作を停止しています。

-   I/O のターゲットに要求を転送できません。

-   呼び出す[ **WdfRequestCancelSentRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)しようとすると、ドライバーが I/O のターゲットに送信された以前の要求をキャンセルします。

ドライバーが呼び出してで要求を完了する必要があります常に場合は、ドライバーのドライバーが、framework から受信した要求オブジェクトの I/O 要求をキャンセル、 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)で、 *の状態*パラメーターの状態の\_キャンセルします。 (ドライバーが呼び出された場合[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)ドライバー呼び出し、要求オブジェクトを作成する[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)の代わりに要求を完了します。)

### <a name="synchronizing-cancellation"></a>同期のキャンセル

同期 I/O 要求をキャンセルするコードについてを参照してください。

-   [キャンセルおよび終了コードを同期します。](synchronizing-cancel-and-completion-code.md)

-   [同期送信済み要求の取り消し](synchronizing-cancellation-of-sent-requests.md)

 

 





