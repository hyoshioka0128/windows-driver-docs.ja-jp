---
title: IRP 処理のさまざまな方法 - チート シート
author: kaushika-msft
description: Irp を処理するさまざまな方法
keywords:
- Irp WDK カーネル、Irp の処理
ms.date: 12/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f037021882b9c45f4101789549d8f22de7802fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828324"
---
# <a name="different-ways-of-handling-irps---cheat-sheet"></a>IRP 処理のさまざまな方法 - チート シート 

通常、Windows Driver Model (WDM) ドライバーは、入力/出力要求パケット (Irp) を他のドライバーに送信します。 ドライバーは独自の IRP を作成し、それを下位のドライバーに送信します。または、ドライバーが、上でアタッチされている別のドライバーから受信した Irp を転送します。 

この記事では、ドライバーがより低いドライバーに Irp を送信し、注釈付きサンプルコードを含むさまざまな方法について説明します。

* シナリオ1-5 は、IRP をディスパッチルーチンから下位のドライバーに転送する方法を示しています。
* シナリオ6-12 では、さまざまな方法で IRP を作成し、別のドライバーに送信する方法について説明します。

さまざまなシナリオを確認する前に、IRP 完了ルーチンが STATUS_MORE_PROCESSING_REQUIRED または STATUS_SUCCESS を返す可能性があることに注意してください。

I/o マネージャーは、状態を調べるときに次の規則を使用します。

* 状態が STATUS_MORE_PROCESSING_REQUIRED の場合は、IRP の完了を停止し、スタックの場所はそのままにして、を返します。
* 状態が STATUS_MORE_PROCESSING_REQUIRED 以外のものである場合は、IRP を上方向へ続行します。

I/o マネージャーは、使用されている STATUS_MORE_PROCESSING_REQUIRED 以外の値を知る必要がないので、STATUS_SUCCESS を使用します (ほとんどのプロセッサアーキテクチャで値0が効率的に読み込まれるため)。

次のコードを読むと、STATUS_CONTINUE_COMPLETION は WDK の STATUS_SUCCESS にエイリアスされていることに注意してください。

```cpp
// This value should be returned from completion routines to continue
// completing the IRP upwards. Otherwise, STATUS_MORE_PROCESSING_REQUIRED
// should be returned.
// 
#define STATUS_CONTINUE_COMPLETION      STATUS_SUCCESS
// 
// Completion routines can also use this enumeration instead of status codes.
// 
typedef enum _IO_COMPLETION_ROUTINE_RESULT {

    ContinueCompletion = STATUS_CONTINUE_COMPLETION,
    StopCompletion = STATUS_MORE_PROCESSING_REQUIRED

} IO_COMPLETION_ROUTINE_RESULT, *PIO_COMPLETION_ROUTINE_RESULT;
```

## <a name="forwarding-an-irp-to-another-driver"></a>IRP を別のドライバーに転送する

### <a name="scenario-1-forward-and-forget"></a>シナリオ 1: 転送と破棄
ドライバーが IRP を転送するだけで、追加のアクションを実行しない場合は、次のコードを使用します。 この場合、ドライバーは完了ルーチンを設定する必要はありません。 ドライバーが最上位のドライバーである場合は、下位のドライバーによって返される状態に応じて、同期的または非同期的に IRP を完了できます。 

```cpp
NTSTATUS
DispatchRoutine_1(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    // 
    // You are not setting a completion routine, so just skip the stack
    // location because it provides better performance.
    // 
    IoSkipCurrentIrpStackLocation (Irp);
    return IoCallDriver(TopOfDeviceStack, Irp);
} 
```

### <a name="scenario-2-forward-and-wait"></a>シナリオ 2: 転送と待機

ドライバーが irp を下位のドライバーに転送し、が返されるのを待って IRP を処理できるようにする場合は、次のコードを使用します。 これは、PNP Irp を処理するときに頻繁に実行されます。 たとえば、 [IRP_MN_START_DEVICE](irp-mn-start-device.md) irp を受信した場合、irp をバスドライバーに転送し、完了するのを待ってから、デバイスを起動する必要があります。 [**IoForwardIrpSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously)を呼び出すと、この操作を簡単に行うことができます。

```cpp
NTSTATUS
DispatchRoutine_2(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    KEVENT   event;
    NTSTATUS status;

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    // 
    // You are setting completion routine, so you must copy
    // current stack location to the next. You cannot skip a location
    // here.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp);

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_2,
                           &event,
                           TRUE,
                           TRUE,
                           TRUE
                           );

    status = IoCallDriver(TopOfDeviceStack, Irp);

    if (status == STATUS_PENDING) {

       KeWaitForSingleObject(&event,
                             Executive, // WaitReason
                             KernelMode, // must be Kernelmode to prevent the stack getting paged out
                             FALSE,
                             NULL // indefinite wait
                             );
       status = Irp->IoStatus.Status;
    }

    // <---- Do your own work here.


    // 
    // Because you stopped the completion of the IRP in the CompletionRoutine
    // by returning STATUS_MORE_PROCESSING_REQUIRED, you must call
    // IoCompleteRequest here.
    // 
    IoCompleteRequest (Irp, IO_NO_INCREMENT);
    return status;

}
NTSTATUS
CompletionRoutine_2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{ 
  if (Irp->PendingReturned == TRUE) {
    // 
    // You will set the event only if the lower driver has returned
    // STATUS_PENDING earlier. This optimization removes the need to
    // call KeSetEvent unnecessarily and improves performance because the
    // system does not have to acquire an internal lock.  
    // 
    KeSetEvent ((PKEVENT) Context, IO_NO_INCREMENT, FALSE);
  }
  // This is the only status you can return. 
  return STATUS_MORE_PROCESSING_REQUIRED;  
} 
```

### <a name="scenario-3-forward-with-a-completion-routine"></a>シナリオ 3: 完了ルーチンを使用して転送する

この場合、ドライバーは完了ルーチンを設定し、IRP を転送してから、下位ドライバーの状態をその状態に戻します。 完了ルーチンを設定する目的は、IRP の内容を元の位置に変更することです。 

```cpp
NTSTATUS
DispathRoutine_3(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    NTSTATUS status;

    // 
    // Because you are setting completion routine, you must copy the
    // current stack location to the next. You cannot skip a location
    // here.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp); 

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_31,// or CompletionRoutine_32
                           NULL,
                           TRUE,
                           TRUE,
                           TRUE
                           );

    return IoCallDriver(TopOfDeviceStack, Irp);
}
```

ディスパッチルーチンから下位のドライバーの状態を返す場合は、次の手順を実行します。

* 完了ルーチンの IRP の状態を変更することはできません。 これは、IRP の IoStatus ブロック (Irp > IoStatus. Status) に設定されている状態値が、下位のドライバーのリターンステータスと同じであることを確認するためです。
* Irp > PendingReturned によって示されているように、IRP の保留状態を反映する必要があります。
* IRP の同期を変更することはできません。

そのため、このシナリオでは、次の2つの有効なバージョンの完了ルーチン (31 と 32) のみが存在します。

```cpp
NTSTATUS
CompletionRoutine_31 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{   

    // 
    // Because the dispatch routine is returning the status of lower driver
    // as is, you must do the following:
    // 
    if (Irp->PendingReturned) {

        IoMarkIrpPending( Irp );
    }

    return STATUS_CONTINUE_COMPLETION ; // Make sure of same synchronicity 
}

NTSTATUS
CompletionRoutine_32 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{   
    // 
    // Because the dispatch routine is returning the status of lower driver
    // as is, you must do the following:
    // 
    if (Irp->PendingReturned) {

        IoMarkIrpPending( Irp );
    }

    //    
    // To make sure of the same synchronicity, complete the IRP here.
    // You cannot complete the IRP later in another thread because the 
    // the dispatch routine is returning the status returned by the lower
    // driver as is.
    // 
    IoCompleteRequest( Irp,  IO_NO_INCREMENT);  

    // 
    // Although this is an unusual completion routine that you rarely see,
    // it is discussed here to address all possible ways to handle IRPs.  
    // 
    return STATUS_MORE_PROCESSING_REQUIRED; 
} 
```

### <a name="scenario-4-queue-for-later-or-forward-and-reuse"></a>シナリオ 4: 後で使用するためのキュー、または転送と再利用

次のコードスニペットは、ドライバーが IRP をキューに配置し、後で処理するか、または IRP を下位ドライバーに転送し、IRP を完了する前に特定の回数だけ再利用する必要がある状況で使用します。 ディスパッチルーチンは、irp が別のスレッドで後で完了する予定のため、保留中の IRP をマークし、ありますを返します。 ここでは、必要に応じて、完了ルーチンが IRP の状態を変更できます (前のシナリオとは異なります)。 

```cpp
NTSTATUS
DispathRoutine_4(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    NTSTATUS status;

    // 
    // You mark the IRP pending if you are intending to queue the IRP
    // and process it later. If you are intending to forward the IRP 
    // directly, use one of the methods discussed earlier in this article.
    // 
    IoMarkIrpPending( Irp );    

    // 
    // For demonstration purposes: this IRP is forwarded to the lower driver.
    // 
    IoCopyCurrentIrpStackLocationToNext(Irp); 

    IoSetCompletionRoutine(Irp,
                           CompletionRoutine_41, // or CompletionRoutine_42
                           NULL,
                           TRUE,
                           TRUE,
                           TRUE
                           ); 
    IoCallDriver(TopOfDeviceStack, Irp);

    // 
    // Because you marked the IRP pending, you must return pending,
    // regardless of the status of returned by IoCallDriver.
    // 
    return STATUS_PENDING ;

}
```

完了ルーチンは、STATUS_CONTINUE_COMPLETION または STATUS_MORE_PROCESSING_REQUIRED を返すことができます。 STATUS_MORE_PROCESSING_REQUIRED は、別のスレッドから IRP を再利用し、後で完了する場合にのみ返されます。

```cpp
NTSTATUS
CompletionRoutine_41(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{ 
    // 
    // By returning STATUS_CONTINUE_COMPLETION , you are relinquishing the 
    // ownership of the IRP. You cannot touch the IRP after this.
    // 
    return STATUS_CONTINUE_COMPLETION ; 
} 


NTSTATUS
CompletionRoutine_42 (
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{  
    // 
    // Because you are stopping the completion of the IRP by returning the
    // following status, you must complete the IRP later.
    // 
    return STATUS_MORE_PROCESSING_REQUIRED ; 
}
```

### <a name="scenario-5-complete-the-irp-in-the-dispatch-routine"></a>シナリオ 5: ディスパッチルーチンで IRP を完了する

このシナリオでは、ディスパッチルーチンで IRP を完了する方法を示します。 

**重要**ディスパッチルーチンで IRP を完了すると、ディスパッチルーチンの戻りステータスは、IRP の IoStatus ブロックで設定されている値の状態 (Irp > IoStatus. Status) と一致する必要があります。

```cpp
NTSTATUS
DispatchRoutine_5(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    // 
    // <-- Process the IRP here.
    // 
    Irp->IoStatus.Status = STATUS_XXX;
    Irp->IoStatus.Information = YYY;
    IoCompletRequest(Irp, IO_NO_INCREMENT);
    return STATUS_XXX;
}
```

## <a name="creating-irps-and-sending-them-to-another-driver"></a>Irp の作成と他のドライバーへの送信

### <a name="introduction"></a>概要

シナリオを確認する前に、ドライバーで作成された同期入出力要求パケット (IRP) と非同期要求の違いを理解しておく必要があります。 

|    同期 (スレッド) IRP                                                                                                                        |    非同期 (非スレッド) IRP                                                                                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    IoBuildSynchronousFsdRequest または IoBuildDeviceIoControlRequest を使用して作成されます。                                                                  |    IoBuildAsynchronousFsdRequest または IoAllocateIrp を使用して作成されます。 これは、ドライバーとドライバーの通信を目的としています。                                 |
|    スレッドは、IRP が完了するまで待機する必要があります。                                                                                                         |    スレッドが IRP の完了を待機する必要がありません。                                                                                                 |
|    これは、それを作成したスレッドに関連付けられます。したがって、名前スレッドの Irp です。 そのため、スレッドが終了すると、i/o マネージャーは IRP をキャンセルします。     |    作成したスレッドに関連付けられていません。                                                                                                       |
|    は、任意のスレッドコンテキストで作成することはできません。                                                                                                 |    は、スレッドが IRP の完了を待機しないため、任意のスレッドコンテキストで作成できます。                                             |
|    I/o マネージャーは、IRP に関連付けられているバッファーを解放するために、post の完了を行います。                                                     |    I/o マネージャーはクリーンアップを実行できません。 ドライバーは、完了ルーチンを提供し、IRP に関連付けられているバッファーを解放する必要があります。          |
|    は、PASSIVE_LEVEL に等しい IRQL レベルで送信される必要があります。                                                                                                |    ターゲットドライバーのディスパッチルーチンが DISPATCH_LEVEL で要求を処理できる場合、DISPATCH_LEVEL 以下の IRQL で送信できます。     |

### <a name="scenario-6-send-a-synchronous-device-control-request-irp_mj_internal_device_controlirp_mj_device_control-by-using-iobuilddeviceiocontrolrequest"></a>シナリオ 6: IoBuildDeviceIoControlRequest を使用して同期デバイス制御要求 (IRP_MJ_INTERNAL_DEVICE_CONTROL/IRP_MJ_DEVICE_CONTROL) を送信する

次のコードは、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) request を呼び出して同期 IOCTL 要求を作成する方法を示しています。  詳細については、「 [IRP_MJ_INTERNAL_DEVICE_CONTROL](irp-mj-internal-device-control.md) and [IRP_MJ_DEVICE_CONTROL](irp-mj-device-control.md)」を参照してください。

```cpp
NTSTATUS
MakeSynchronousIoctl(
    IN PDEVICE_OBJECT    TopOfDeviceStack,
    IN ULONG         IoctlControlCode,
    PVOID             InputBuffer,
    ULONG             InputBufferLength,
    PVOID             OutputBuffer,
    ULONG             OutputBufferLength
    )
/*++

Arguments:

    TopOfDeviceStack- 

    IoctlControlCode              - Value of the IOCTL request

    InputBuffer        - Buffer to be sent to the TopOfDeviceStack

    InputBufferLength  - Size of buffer to be sent to the TopOfDeviceStack

    OutputBuffer       - Buffer for received data from the TopOfDeviceStack

    OutputBufferLength - Size of receive buffer from the TopOfDeviceStack

Return Value:

    NT status code

--*/ 
{
    KEVENT              event;
    PIRP                irp;
    IO_STATUS_BLOCK     ioStatus;
    NTSTATUS status;

    // 
    // Creating Device control IRP and send it to the another
    // driver without setting a completion routine.
    // 

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    irp = IoBuildDeviceIoControlRequest (
                            IoctlControlCode,
                            TopOfDeviceStack,
                            InputBuffer,
                            InputBufferLength,
                            OutputBuffer,
                            OutputBufferLength,
                            FALSE, // External
                            &event,
                            &ioStatus);

    if (NULL == irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }


    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {
        // 
        // You must wait here for the IRP to be completed because:
        // 1) The IoBuildDeviceIoControlRequest associates the IRP with the
        //     thread and if the thread exits for any reason, it would cause the IRP
        //     to be canceled. 
        // 2) The Event and IoStatus block memory is from the stack and we
        //     cannot go out of scope.
        // This event will be signaled by the I/O manager when the
        // IRP is completed.
        // 
        status = KeWaitForSingleObject(
                     &event,
                     Executive, // wait reason
                     KernelMode, // To prevent stack from being paged out.
                     FALSE,     // You are not alertable
                     NULL);     // No time out !!!!

        status = ioStatus.Status;                     
    }

    return status;
}
```

### <a name="scenario-7-send-a-synchronous-device-control-ioctl-request-and-cancel-it-if-not-completed-in-a-certain-time-period"></a>シナリオ 7: 同期デバイス制御 (IOCTL) 要求を送信し、一定の期間内に完了していない場合はキャンセルする 
このシナリオは、要求が完了するまで無期限に待機するのではなく、ユーザーが指定した時間待機し、待機がタイムアウトした場合に IOCTL 要求を安全にキャンセルすることを除いて、前のシナリオに似ています。 

```cpp
typedef enum {

   IRPLOCK_CANCELABLE,
   IRPLOCK_CANCEL_STARTED,
   IRPLOCK_CANCEL_COMPLETE,
   IRPLOCK_COMPLETED

} IRPLOCK;
// 
// An IRPLOCK allows for safe cancellation. The idea is to protect the IRP
// while the canceller is calling IoCancelIrp. This is done by wrapping the
// call in InterlockedExchange(s). The roles are as follows:
// 
// Initiator/completion: Cancelable --> IoCallDriver() --> Completed
// Canceller: CancelStarted --> IoCancelIrp() --> CancelCompleted
// 
// No cancellation:
//   Cancelable-->Completed
// 
// Cancellation, IoCancelIrp returns before completion:
//   Cancelable --> CancelStarted --> CancelCompleted --> Completed
// 
// Canceled after completion:
//   Cancelable --> Completed -> CancelStarted
// 
// Cancellation, IRP completed during call to IoCancelIrp():
//   Cancelable --> CancelStarted -> Completed --> CancelCompleted
// 
//  The transition from CancelStarted to Completed tells the completer to block
//  postprocessing (IRP ownership is transferred to the canceller). Similarly,
//  the canceller learns it owns IRP postprocessing (free, completion, etc)
//  during a Completed->CancelCompleted transition.
// 


NTSTATUS
MakeSynchronousIoctlWithTimeOut(
    IN PDEVICE_OBJECT    TopOfDeviceStack,
    IN ULONG         IoctlControlCode,
    PVOID             InputBuffer,
    ULONG             InputBufferLength,
    PVOID             OutputBuffer,
    ULONG             OutputBufferLength,
    IN  ULONG               Milliseconds
    )
/*++

Arguments:

    TopOfDeviceStack   - 

    IoctlControlCode   - Value of the IOCTL request.

    InputBuffer        - Buffer to be sent to the TopOfDeviceStack.

    InputBufferLength  - Size of buffer to be sent to the TopOfDeviceStack.

    OutputBuffer       - Buffer for received data from the TopOfDeviceStack.

    OutputBufferLength - Size of receive buffer from the TopOfDeviceStack.

    Milliseconds       - Timeout value in Milliseconds

Return Value:

    NT status code

--*/ 
{
    NTSTATUS status;
    PIRP irp;
    KEVENT event;
    IO_STATUS_BLOCK ioStatus;
    LARGE_INTEGER dueTime;
    IRPLOCK lock;

    KeInitializeEvent(&event, NotificationEvent, FALSE);

    irp = IoBuildDeviceIoControlRequest (
                    IoctlControlCode,
                    TopOfDeviceStack,
                    InputBuffer,
                    InputBufferLength,
                    OutputBuffer,
                    OutputBufferLength,
                    FALSE, // External ioctl
                    &event,
                    &ioStatus);



    if (irp == NULL) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    lock = IRPLOCK_CANCELABLE;

    IoSetCompletionRoutine(
                    irp,
                    MakeSynchronousIoctlWithTimeOutCompletion,
                    &lock,
                    TRUE,
                    TRUE,
                    TRUE
                    );

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

        dueTime.QuadPart = -10000 * Milliseconds;

        status = KeWaitForSingleObject(
                            &event,
                            Executive,
                            KernelMode,
                            FALSE,
                            &dueTime
                            );

        if (status == STATUS_TIMEOUT) {

            if (InterlockedExchange((PVOID)&lock, IRPLOCK_CANCEL_STARTED) == IRPLOCK_CANCELABLE) {

                // 
                // You got it to the IRP before it was completed. You can cancel
                // the IRP without fear of losing it, because the completion routine
                // does not let go of the IRP until you allow it.
                // 
                IoCancelIrp(irp);

                // 
                // Release the completion routine. If it already got there,
                // then you need to complete it yourself. Otherwise, you got
                // through IoCancelIrp before the IRP completed entirely.
                // 
                if (InterlockedExchange(&lock, IRPLOCK_CANCEL_COMPLETE) == IRPLOCK_COMPLETED) {
                    IoCompleteRequest(irp, IO_NO_INCREMENT);
                }
            }

            KeWaitForSingleObject(&event, Executive, KernelMode, FALSE, NULL);

            ioStatus.Status = status; // Return STATUS_TIMEOUT

        } else {

            status = ioStatus.Status;
        }
    }

    return status;
}

NTSTATUS
MakeSynchronousIoctlWithTimeOutCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PLONG lock;

    lock = (PLONG) Context;

    if (InterlockedExchange(lock, IRPLOCK_COMPLETED) == IRPLOCK_CANCEL_STARTED) {
        // 
        // Main line code has got the control of the IRP. It will
        // now take the responsibility of completing the IRP. 
        // Therefore...
        return STATUS_MORE_PROCESSING_REQUIRED;
    }

    return STATUS_CONTINUE_COMPLETION ;
}
```

### <a name="scenario-8-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-status_continue_completion"></a>シナリオ 8: IoBuildSynchronousFsdRequest を使用して同期非 IOCTL 要求を送信する-完了ルーチンが STATUS_CONTINUE_COMPLETION を返す
次のコードは、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)を呼び出して、非同期の非 IOCTL 要求を行う方法を示しています。 ここに示す手法は、シナリオ6に似ています。

```cpp
NTSTATUS
MakeSynchronousNonIoctlRequest (
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

Return Value:

    NT status code


--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    IO_STATUS_BLOCK     ioStatus;
    PVOID context;

    startingOffset.QuadPart = (LONGLONG) 0;
    // 
    // Allocate memory for any context information to be passed
    // to the completion routine.
    // 
    context = ExAllocatePoolWithTag(NonPagedPool, sizeof(ULONG), 'ITag');
    if(!context) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    KeInitializeEvent(&event,  NotificationEvent,   FALSE);

    irp = IoBuildSynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,


                &startingOffset, // Optional
                &event,
                &ioStatus
                ); 

    if (NULL == irp) {
        ExFreePool(context);
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                   MakeSynchronousNonIoctlRequestCompletion,
                   context,
                   TRUE,
                   TRUE,
                   TRUE);

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

       status = KeWaitForSingleObject(
                            &event,
                            Executive,
                            KernelMode,
                            FALSE, // Not alertable
                            NULL);
        status = ioStatus.Status;
    }

    return status;
}
NTSTATUS
MakeSynchronousNonIoctlRequestCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    if (Context) {
        ExFreePool(Context);
    }
    return STATUS_CONTINUE_COMPLETION ;

}
```

### <a name="scenario-9-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-status_more_processing_required"></a>シナリオ 9: IoBuildSynchronousFsdRequest を使用して同期非 IOCTL 要求を送信する-完了ルーチンが STATUS_MORE_PROCESSING_REQUIRED を返す 
このシナリオとシナリオ8の唯一の違いは、完了ルーチンが STATUS_MORE_PROCESSING_REQUIRED を返すことです。 

```cpp
NTSTATUS MakeSynchronousNonIoctlRequest2(
    PDEVICE_OBJECT TopOfDeviceStack,
    PVOID WriteBuffer,
    ULONG NumBytes
    )
/*++ Arguments:
    TopOfDeviceStack

    WriteBuffer     - Buffer to be sent to the TopOfDeviceStack.

    NumBytes        - Size of buffer to be sent to the TopOfDeviceStack.

Return Value:
    NT status code
--*/
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    IO_STATUS_BLOCK ioStatus;
    BOOLEAN         isSynchronous = TRUE;

    startingOffset.QuadPart = (LONGLONG) 0;
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    irp = IoBuildSynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                &event,
                &ioStatus
                );

    if (NULL == irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                MakeSynchronousNonIoctlRequestCompletion2,
                (PVOID)&event,
                TRUE,
                TRUE,
                TRUE);

    status = IoCallDriver(TopOfDeviceStack, irp);

    if (status == STATUS_PENDING) {

        KeWaitForSingleObject(&event,
                              Executive,
                              KernelMode,
                              FALSE, // Not alertable
                              NULL);
        status = irp->IoStatus.Status;
        isSynchronous = FALSE;
    }

    //
    // Because you have stopped the completion of the IRP, you must
    // complete here and wait for it to be completed by waiting
    // on the same event again, which will be signaled by the I/O
    // manager.
    // NOTE: you cannot queue the IRP for
    // reuse by calling IoReuseIrp because it does not break the
    // association of this IRP with the current thread.
    //

    KeClearEvent(&event);
    IoCompleteRequest(irp, IO_NO_INCREMENT);

    //
    // We must wait here to prevent the event from going out of scope.
    // I/O manager will signal the event and copy the status to our
    // IoStatus block for synchronous IRPs only if the return status is not
    // an error. For asynchronous IRPs, the above mentioned copy operation
    // takes place regardless of the status value.
    //

    if (!(NT_ERROR(status) && isSynchronous)) {
        KeWaitForSingleObject(&event,
                              Executive,
                              KernelMode,
                              FALSE, // Not alertable
                              NULL);
    }
    return status;
}

NTSTATUS MakeSynchronousNonIoctlRequestCompletion2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context )
{
    if (Irp->PendingReturned) {
        KeSetEvent ((PKEVENT) Context, IO_NO_INCREMENT, FALSE);
    }
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-10-send-an-asynchronous-request-by-using-iobuildasynchronousfsdrequest"></a>シナリオ 10: IoBuildAsynchronousFsdRequest を使用して非同期要求を送信する 
このシナリオでは、 [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を呼び出して非同期要求を行う方法を示します。 

非同期要求では、要求を行ったスレッドは、IRP が完了するまで待機する必要がありません。 Irp はスレッドに関連付けられていないため、任意のスレッドコンテキストで IRP を作成できます。 IRP を再利用する予定がない場合は、完了ルーチンを提供し、完了ルーチンでバッファーと IRP を解放する必要があります。 これは、i/o マネージャーが、ドライバーによって作成された非同期 Irp ( **IoBuildAsynchronousFsdRequest**と**Ioallocateirp**で作成) の完了後のクリーンアップを実行できないためです。 

```cpp
NTSTATUS
MakeAsynchronousRequest (
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    PIO_STACK_LOCATION  nextStack;
    PVOID context;

    startingOffset.QuadPart = (LONGLONG) 0;

    irp = IoBuildAsynchronousFsdRequest(
                IRP_MJ_WRITE,
                TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                NULL
                ); 

    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // 
    // Allocate memory for context structure to be passed to the completion routine.
    // 
    context = ExAllocatePoolWithTag(NonPagedPool, sizeof(ULONG_PTR), 'ITag');
    if (NULL == context) {
        IoFreeIrp(irp);   
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    IoSetCompletionRoutine(irp,
                   MakeAsynchronousRequestCompletion,
                   context,
                   TRUE,
                   TRUE,
                   TRUE);
    // 
    // If you want to change any value in the IRP stack, you must
    // first obtain the stack location by calling IoGetNextIrpStackLocation.
    // This is the location that is initialized by the IoBuildxxx requests and  
    // is the one that the target device driver is going to view.
    // 
    nextStack = IoGetNextIrpStackLocation(irp);
    // 
    // Change the MajorFunction code to something appropriate.
    // 
    nextStack->MajorFunction = IRP_MJ_SCSI;

    (void) IoCallDriver(TopOfDeviceStack, irp);

    return STATUS_SUCCESS;
}
NTSTATUS
MakeAsynchronousRequestCompletion(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;

    // 
    // If the target device object is set up to do buffered i/o 
    // (TopOfDeviceStack->Flags and DO_BUFFERED_IO), then 
    // IoBuildAsynchronousFsdRequest request allocates a system buffer
    // for read and write operation. If you stop the completion of the IRP
    // here, you must free that buffer.
    // 

    if(Irp->AssociatedIrp.SystemBuffer && (Irp->Flags & IRP_DEALLOCATE_BUFFER) ) {
            ExFreePool(Irp->AssociatedIrp.SystemBuffer);
    }

    // 
    // If the target device object is set up do direct i/o (DO_DIRECT_IO), then 
    // IoBuildAsynchronousFsdRequest creates an MDL to describe the buffer
    // and locks the pages. If you stop the completion of the IRP, you must unlock
    // the pages and free the MDL.
    // 

    else if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    if(Context) {
        ExFreePool(Context);
    }



    // 
    // If you intend to queue the IRP and reuse it for another request,
    // make sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 
    IoFreeIrp(Irp);

    // 
    // NOTE: this is the only status that you can return for driver-created asynchronous IRPs.
    // 
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-11-send-an-asynchronous-request-by-using-ioallocateirp"></a>シナリオ 11: IoAllocateIrp を使用して非同期要求を送信する

このシナリオは、前のシナリオに似ています。ただし、このシナリオでは、 [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を呼び出す代わりに、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)関数を使用して IRP を作成します。

```cpp
NTSTATUS
MakeAsynchronousRequest2(
    PDEVICE_OBJECT   TopOfDeviceStack,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    TopOfDeviceStack - 

    WriteBuffer       - Buffer to be sent to the TopOfDeviceStack.

    NumBytes  - Size of buffer to be sent to the TopOfDeviceStack.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    KEVENT          event;
    PIO_STACK_LOCATION  nextStack;

    startingOffset.QuadPart = (LONGLONG) 0;

    // 
    // Start by allocating the IRP for this request.  Do not charge quota
    // to the current process for this IRP.
    // 

    irp = IoAllocateIrp( TopOfDeviceStack->StackSize, FALSE );
    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

     // 
    // Obtain a pointer to the stack location of the first driver that will be
    // invoked.  This is where the function codes and the parameters are set.
    // 

    nextStack = IoGetNextIrpStackLocation( irp );
    nextStack->MajorFunction = IRP_MJ_WRITE;
    nextStack->Parameters.Write.Length = NumBytes;
    nextStack->Parameters.Write.ByteOffset= startingOffset;


    if(TopOfDeviceStack->Flags & DO_BUFFERED_IO) {

        irp->AssociatedIrp.SystemBuffer = WriteBuffer;
        irp->MdlAddress = NULL;

    } else if (TopOfDeviceStack->Flags & DO_DIRECT_IO) {
        // 
        // The target device supports direct I/O operations.  Allocate
        // an MDL large enough to map the buffer and lock the pages into
        // memory.
        // 
        irp->MdlAddress = IoAllocateMdl( WriteBuffer,
                                         NumBytes,
                                         FALSE,
                                         FALSE,
                                         (PIRP) NULL );
        if (irp->MdlAddress == NULL) {
            IoFreeIrp( irp );
            return STATUS_INSUFFICIENT_RESOURCES;
        }

        try {

            MmProbeAndLockPages( irp->MdlAddress,
                                 KernelMode,
                                 (LOCK_OPERATION) (nextStack->MajorFunction == IRP_MJ_WRITE ? IoReadAccess : IoWriteAccess) );

        } except(EXCEPTION_EXECUTE_HANDLER) {

              if (irp->MdlAddress != NULL) {
                  IoFreeMdl( irp->MdlAddress );
              }
              IoFreeIrp( irp );
              return  GetExceptionCode();

        }
    }   

    IoSetCompletionRoutine(irp,
                   MakeAsynchronousRequestCompletion2,
                   NULL,
                   TRUE,
                   TRUE,
                   TRUE);

    (void) IoCallDriver(TargetDeviceObject, irp);

    return STATUS_SUCCESS;
}

NTSTATUS
MakeAsynchronousRequestCompletion2(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;

    // 
    // Free any associated MDL.
    // 

    if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    // 
    // If you intend to queue the IRP and reuse it for another request,
    // make sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 

    IoFreeIrp(Irp);

    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

### <a name="scenario-12-send-an-asynchronous-request-and-cancel-it-in-a-different-thread"></a>シナリオ 12: 非同期要求を送信して別のスレッドで取り消す 
このシナリオでは、要求の完了を待たずに、一度に1つの要求を下位のドライバーに送信する方法について説明します。また、他のスレッドからいつでも要求をキャンセルすることもできます。 

次に示すように、IRP とその他の変数を記憶して、デバイスの拡張機能や、デバイスに対してグローバルなコンテキスト構造でこの作業を行うことができます。 IRP の状態は、デバイス拡張機能の IRPLOCK 変数を使用して追跡されます。 IrpEvent は、次の要求を行う前に、IRP が完全に完了 (または解放) されるようにするために使用されます。 

このイベントは、要求を完了する前に保留中の Irp がないことを確認する必要がある場合に、 [IRP_MN_REMOVE_DEVICE](irp-mn-remove-device.md)と[IRP_MN_STOP_DEVICE の PNP](irp-mn-stop-device.md)要求を処理するときにも役立ちます。 このイベントは、AddDevice または他の初期化ルーチンで同期イベントとして初期化するときに最適に動作します。

```cpp
typedef struct _DEVICE_EXTENSION{
    ..
    PDEVICE_OBJECT TopOfDeviceStack;
    PIRP PendingIrp; 
    IRPLOCK IrpLock; // You need this to track the state of the IRP.
    KEVENT IrpEvent; // You need this to synchronize various threads.
    ..
} DEVICE_EXTENSION, *PDEVICE_EXTENSION;
                 </pre><pre class="code">
InitializeDeviceExtension( PDEVICE_EXTENSION  DeviceExtension)
{
    KeInitializeEvent(&DeviceExtension->IrpEvent, SynchronizationEvent, TRUE); 
}

NTSTATUS
MakeASynchronousRequest3(
    PDEVICE_EXTENSION  DeviceExtension,
    PVOID               WriteBuffer,
    ULONG               NumBytes
    )
/*++
Arguments:

    DeviceExtension - 

    WriteBuffer       - Buffer to be sent to the TargetDeviceObject.

    NumBytes  - Size of buffer to be sent to the TargetDeviceObject.

--*/ 
{
    NTSTATUS        status;
    PIRP            irp;
    LARGE_INTEGER   startingOffset;
    PIO_STACK_LOCATION  nextStack;

    // 
    // Wait on the event to make sure that PendingIrp
    // field is free to be used for the next request. If you do
    // call this function in the context of the user thread,
    // make sure to call KeEnterCriticialRegion before the wait to protect 
    // the thread from getting suspended while holding a lock.
    // 
    KeWaitForSingleObject( &DeviceExtension->IrpEvent,
                           Executive,
                           KernelMode,
                           FALSE,
                           NULL );

    startingOffset.QuadPart = (LONGLONG) 0;
    // 
    // If the IRP is used for the same purpose every time, you can just create the IRP in the
    // Initialization routine one time and reuse it by calling IoReuseIrp. 
    // The only thing that you have to do in the routines in this article 
    // is remove the lines that call IoFreeIrp and set the PendingIrp
    // field to NULL. If you do so, make sure that you free the IRP 
    // in the PNP remove handler.
    // 
    irp = IoBuildAsynchronousFsdRequest(
                IRP_MJ_WRITE,
                DeviceExtension->TopOfDeviceStack,
                WriteBuffer,
                NumBytes,
                &startingOffset, // Optional
                NULL
                ); 

    if (NULL == irp) {

        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // 
    // Initialize the fields relevant fields in the DeviceExtension
    // 
    DeviceExtension->PendingIrp = irp;
    DeviceExtension->IrpLock = IRPLOCK_CANCELABLE;

    IoSetCompletionRoutine(irp,
                   MakeASynchronousRequestCompletion3,
                   DeviceExtension,
                   TRUE,
                   TRUE,
                   TRUE);
    // 
    // If you want to change any value in the IRP stack, you must
    // first obtain the stack location by calling IoGetNextIrpStackLocation.
    // This is the location that is initialized by the IoBuildxxx requests and  
    // is the one that the target device driver is going to view.
    // 

    nextStack = IoGetNextIrpStackLocation(irp);

    // 
    // You could change the MajorFunction code to something appropriate.
    // 
    nextStack->MajorFunction = IRP_MJ_SCSI;

    (void) IoCallDriver(DeviceExtension->TopOfDeviceStack, irp);

    return STATUS_SUCCESS;
}

NTSTATUS
MakeASynchronousRequestCompletion3(
    IN PDEVICE_OBJECT   DeviceObject,
    IN PIRP             Irp,
    IN PVOID            Context
    )
{
    PMDL mdl, nextMdl;
    PDEVICE_EXTENSION deviceExtension = Context;

    // 
    // If the target device object is set up to do buffered i/o 
    // (TargetDeviceObject->Flags & DO_BUFFERED_IO), then 
    // IoBuildAsynchronousFsdRequest request allocates a system buffer
    // for read and write operation. If you stop the completion of the IRP
    // here, you must free that buffer.
    // 

    if(Irp->AssociatedIrp.SystemBuffer && (Irp->Flags & IRP_DEALLOCATE_BUFFER) ) {
            ExFreePool(Irp->AssociatedIrp.SystemBuffer);
    }

    // 
    // If the target device object is set up to do direct i/o (DO_DIRECT_IO), then 
    // IoBuildAsynchronousFsdRequest creates an MDL to describe the buffer
    // and locks the pages. If you stop the completion of the IRP, you must unlock
    // the pages and free the MDL.
    // 

    if (Irp->MdlAddress != NULL) {
        for (mdl = Irp->MdlAddress; mdl != NULL; mdl = nextMdl) {
            nextMdl = mdl->Next;
            MmUnlockPages( mdl ); IoFreeMdl( mdl ); // This function will also unmap pages.
        }
        Irp->MdlAddress = NULL;
    }

    if (InterlockedExchange((PVOID)&deviceExtension->IrpLock, IRPLOCK_COMPLETED) 
                    == IRPLOCK_CANCEL_STARTED) {
        // 
        // Main line code has got the control of the IRP. It will
        // now take the responsibility of freeing the IRP. 
        // Therefore...
        return STATUS_MORE_PROCESSING_REQUIRED;
    }

    // 
    // If you intend to queue the IRP and reuse it for another request, make
    // sure you call IoReuseIrp(Irp, STATUS_SUCCESS) before you reuse.
    // 
    IoFreeIrp(Irp);
    deviceExtension->PendingIrp = NULL; // if freed
    // 
    // Signal the event so that the next thread in the waiting list
    // can send the next request.
    // 
    KeSetEvent (&deviceExtension->IrpEvent, IO_NO_INCREMENT, FALSE);

    return STATUS_MORE_PROCESSING_REQUIRED;
}

VOID
CancelPendingIrp(
    PDEVICE_EXTENSION DeviceExtension
    )
/*++
    This function tries to cancel the PendingIrp if it is not already completed.
    Note that the IRP may not be completed and freed when the
    function returns. Therefore, if you are calling this from your PNP Remove device handle,
    you must wait on the IrpEvent to make sure the IRP is indeed completed
    before successfully completing the remove request and allowing the driver to unload.
--*/ 
{ 
     if (InterlockedExchange((PVOID)&DeviceExtension->IrpLock, IRPLOCK_CANCEL_STARTED) == IRPLOCK_CANCELABLE) {

        // 
        // You got it to the IRP before it was completed. You can cancel
        // the IRP without fear of losing it, as the completion routine
        // will not let go of the IRP until you say so.
        // 
        IoCancelIrp(DeviceExtension->PendingIrp);
        // 
        // Release the completion routine. If it already got there,
        // then you need to free it yourself. Otherwise, you got
        // through IoCancelIrp before the IRP completed entirely.
        // 
        if (InterlockedExchange((PVOID)&DeviceExtension->IrpLock, IRPLOCK_CANCEL_COMPLETE) == IRPLOCK_COMPLETED) {
            IoFreeIrp(DeviceExtension->PendingIrp);
            DeviceExtension->PendingIrp = NULL;
            KeSetEvent(&DeviceExtension->IrpEvent, IO_NO_INCREMENT, FALSE);
        }

     }

    return ;
}
```

## <a name="references"></a>参照先 
* Walter Oney。 プログラミング Windows Driver Model、第5章を参照してください。
