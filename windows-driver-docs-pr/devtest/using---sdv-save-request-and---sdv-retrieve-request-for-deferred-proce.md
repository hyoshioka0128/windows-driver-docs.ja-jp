---
title: __Sdv_save_request と __sdv_retrieve_request 遅延プロシージャ呼び出しを使用します。
description: 遅延プロシージャ呼び出しのための __sdv_save_request と __sdv_retrieve_request の使用
ms.assetid: 14d3a022-3e74-4526-9bf5-fee1ce36ac9e
keywords:
- __sdv_save_request
- __sdv_retrieve_request
- DeferredRequestCompleted
- AliasWithinTimerDpc
- AliasWithinDispatch
- Dpc の分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2f13e5ab001712cf45dd8cee14d4181b923691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363786"
---
# <a name="using-sdvsaverequest-and-sdvretrieverequest-for-deferred-procedure-calls"></a>使用して\_ \_sdv\_保存\_要求と\_ \_sdv\_取得\_遅延プロシージャ呼び出しの要求


フレームワークの要求オブジェクトを追跡することは困難であるために、プロシージャ呼び出し (Dpc) の存在する課題 Static Driver Verifier (SDV) を延期できます。 1 つの難易度は、要求は、グローバルのポインターから、通常、キューのコンテキストまたはから作業項目を取得する必要があります。 この問題を克服するために、Static Driver Verifier が 2 つの関数を提供します **\_ \_sdv\_保存\_要求**、および **\_ \_sdv。\_取得\_要求**します。 これらの関数は、SDV を追跡する要求に遅延の要求をマップします。

**\_\_Sdv\_保存\_要求**、および **\_\_sdv\_取得\_要求**関数がある、次の構文。

```
__sdv_save_request( request ) 
```

```
__sdv_retrieve_request( request ) 
```

場所*要求*framework 要求オブジェクトを識別するハンドルを指定できます。

これらの関数は、静的分析ツールでのみ使用されます。 関数は、コンパイラによって無視されます。

次のコード例に示す方法、  **\_ \_sdv\_保存\_要求**と\_  **\_sdv\_の取得\_要求**SDV は、遅延の要求をマップできるように関数を使用して、SDV をガイドします。 SDV は、このマッピングを使用して確認する、 [DeferredRequestCompleted](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-deferredrequestcompleted)ルール。 DeferredRequestCompleted ルールである必要があります **\_ \_sdv\_保存\_要求**と\_  **\_sdv\_取得\_要求**コードに表示されます。 2 つのドライバーのプロパティ規則がある (**AliasWithinDispatch**、 **AliasWithinTimerDpc**) の存在を検索するように、  **\_ \_sdv\_保存\_要求**と\_  **\_sdv\_取得\_要求**関数。

次のコード例は、関数で*EchoEvtIoRead*は、 [ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)で framework 要求オブジェクトへのハンドルを保存するイベントのコールバック関数、キューのコンテキストの領域。 関数は、 *EchoEvtTimerFunc*は、 [ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)イベント コールバック関数を取得します。

```
VOID
EchoEvtIoRead(
 )in WDFQUEUE   Queue,
 __in WDFREQUEST Request,
 __in size_t      Length
    )
{
/* ..................... */
    // Mark the request as cancelable
    WdfRequestMarkCancelable(Request, EchoEvtRequestCancel);
 
 
    // Defer the completion to another thread from the timer DPC and save the handle to the framework request object by using the __sdv_save_request function. 
    queueContext->CurrentRequest = Request;    
 __sdv_save_request(Request);

    queueContext->CurrentStatus  = Status;

    return;
}
```

コード例を次に示します、  **\_ \_sdv\_取得\_要求**SDV の完了を追跡できるように、関数は、既存の要求をマップします。

```
VOID
EchoEvtTimerFunc(
    IN WDFTIMER     Timer
    )
{...................................................
    queue = WdfTimerGetParentObject(Timer);
    queueContext = QueueGetContext(queue);

    //
    // The DPC is automatically synchronized to the queue lock,
    // so this prevents race conditions from occurring without explicit driver-managed locking. The __sdv_retrieve_request function is used so that SDV can restore the deferred request in the timer DPC. Because we know that this deferred request is valid (because it has been previously saved), the __analysis_assume function is used to suppress false defects that might otherwise result in this code path.

    //
 __sdv_retrieve_request(queueContext->CurrentRequest);
    Request = queueContext->CurrentRequest;
 __analysis_assume(Request != NULL);
    if( Request != NULL ) {

        //
        // Try to remove cancel status from the request.
        //
        // The request is not completed if it is already canceled
        // because the EchoEvtIoCancel function has run, or is about to run,
        // and we are racing with it. 

        Status = WdfRequestUnmarkCancelable(Request);
// Because we know that the request is not NULL in this code path and that the request is no longer marked cancelable, we can use the __analysis_assume function to suppress the reporting of a false defect. 

 __analysis_assume(Status != STATUS_CANCELLED);
        if( Status != STATUS_CANCELLED ) {

            queueContext->CurrentRequest = NULL;
            Status = queueContext->CurrentStatus;

            KdPrint(("CustomTimerDPC Completing request 0x%p, Status 0x%x \n", Request,Status));

            WdfRequestComplete(Request, Status);
        }
        else {
            KdPrint(("CustomTimerDPC Request 0x%p is STATUS_CANCELLED, not completing\n",
                                Request));
        }
    }

    return;
}
```

 

 





