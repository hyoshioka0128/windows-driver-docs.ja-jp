---
title: 遅延プロシージャ呼び出しには __sdv_save_request と __sdv_retrieve_request を使用する
description: 遅延プロシージャ呼び出しに __sdv_save_request と __sdv_retrieve_request を使用する
ms.assetid: 14d3a022-3e74-4526-9bf5-fee1ce36ac9e
keywords:
- __sdv_save_request
- __sdv_retrieve_request
- DeferredRequestCompleted
- AliasWithinTimerDpc
- エイリアスのディスパッチ
- Dpc の分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1d99c50749bacc4cdc4f311a34469bbd7db7ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839257"
---
# <a name="using-__sdv_save_request-and-__sdv_retrieve_request-for-deferred-procedure-calls"></a>\_\_sdv\_使用して\_要求を保存し \_sdv\_遅延プロシージャ呼び出しの\_要求を取得する\_


遅延プロシージャ呼び出し (Dpc) では、フレームワークの要求オブジェクトを追跡するのが困難なため、静的ドライバー検証ツール (SDV) に問題があります。 1つの問題は、グローバルポインターから要求を取得する必要があることです。通常はキューコンテキストから、または作業項目から要求を取得する必要があります。 この問題を回避するために、静的なドライバーの検証ツールでは、 **\_\_sdv\_の\_要求の保存**と\_\_**sdv\_\_要求の取得**という2つの機能が提供されています。 これらの関数は、遅延要求を SDV が追跡できる要求にマップします。

**\_\_sdv\_に\_要求を保存**し、\_**sdv\_取得\_要求**関数には次の構文があります。\_

```
__sdv_save_request( request ) 
```

```
__sdv_retrieve_request( request ) 
```

ここで、 *request*は任意のフレームワーク要求オブジェクトへのハンドルです。

これらの関数は、スタティック分析ツールでのみ使用されます。 関数は、コンパイラによって無視されます。

次のコード例では、sdv\_\_sdv を使用して **\_要求を保存**し、\_\_**sdv\_取得\_要求**関数を使用して sdv を\_する方法を示します。これにより、sdv が遅延要求をマップできるようになります。 SDV は、このマッピングを使用して[DeferredRequestCompleted](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-deferredrequestcompleted)規則を確認できます。 DeferredRequestCompleted ルールでは、 **\_\_sdv\_\_要求を保存**し、\_**sdv\_取得\_要求**をコードに表示する必要があります。\_ **\_sdv\_\_** の存在を確認し、\_要求を保存して \_sdv\_取得\_する、2つのドライバープロパティ規則 (エイリアスによる**ディスパッチ**、AliasWithinTimerDpc) があり **@no要求関数 (_s)** 。\_

次のコード例では、関数*EchoEvtIoRead*は、フレームワークの要求オブジェクトへのハンドルをキューのコンテキスト領域に保存する[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)イベントコールバック関数です。 関数*EchoEvtTimerFunc*は、それを取得する[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)イベントコールバック関数です。

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

次のコード例では、 **\_\_sdv\_取得\_要求**関数が既存の要求をマップして、sdv が完了を追跡できるようにする方法を示します。

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

 

 





