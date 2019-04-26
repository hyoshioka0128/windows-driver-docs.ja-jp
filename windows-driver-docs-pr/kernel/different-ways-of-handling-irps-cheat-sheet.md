---
title: IRP 処理のさまざまな方法 - チート シート
author: kaushika-msft
description: さまざまな Irp の処理方法
keywords:
- Irp WDK カーネル、Irp の処理
ms.date: 12/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 555dc8d8fb051791959fe6492633481888f1fc87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342696"
---
# <a name="different-ways-of-handling-irps---cheat-sheet"></a>IRP 処理のさまざまな方法 - チート シート 

通常、Windows Driver Model (WDM) ドライバーは、他のドライバーに入力/出力要求パケット (Irp) を送信します。 ドライバーが IRP を独自に作成し、下位のドライバーに送信します。 または、ドライバーは Irp の上に接続されている別のドライバーから受信するに転送します。 

この記事では、ドライバーは Irp を下位のドライバーに送信して、注釈付きのサンプル コードが含まれるさまざまな方法について説明します。

* シナリオ 1 ~ 5 は、下位のドライバーにディスパッチ ルーチンから IRP を転送する方法の詳細についてです。
* 6 ~ 12 のシナリオでは、さまざまな方法は IRP を作成して、別のドライバーに送信することについて説明します。

さまざまなシナリオを検証する前に、STATUS_MORE_PROCESSING_REQUIRED または STATUS_SUCCESS IRP の完了ルーチンが返すことができますに注意してください。

I/O マネージャーは、状態を確認するときに、次の規則を使用します。

* 状態が STATUS_MORE_PROCESSING_REQUIRED、停止、IRP の完了の場合は、スタックの場所を変更しないままにし、返します。
* ステータスが STATUS_MORE_PROCESSING_REQUIRED 以外の場合は、上方向 IRP の完了を続行します。

I/O マネージャーが使用されている STATUS_MORE_PROCESSING_REQUIRED 以外の値を把握する必要はありません、ため (値 0 がほとんどのプロセッサ アーキテクチャに効率的に読み込まれる) ために STATUS_SUCCESS を使用します。

次のコードを読み、STATUS_CONTINUE_COMPLETION がエイリアスは WDK に STATUS_SUCCESS に注意してください。

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

## <a name="forwarding-an-irp-to-another-driver"></a>別のドライバーは IRP の転送

### <a name="scenario-1-forward-and-forget"></a>シナリオ 1:転送し、もご活用ください。
ドライバーは、ダウン IRP を転送し、追加操作は不要にだけ必要がある場合は、次のコードを使用します。 ドライバーは、完了ルーチンをここで設定する必要はありません。 ドライバーが最上位レベルのドライバーの場合は、IRP が行うことができます同期または非同期では、下位のドライバーによって返される状態に応じて。 

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

### <a name="scenario-2-forward-and-wait"></a>例 2:前方参照と待機

ドライバーは、下位のドライバーに IRP を転送し、返す IRP を処理できるようにするまで待機する必要がある場合は、次のコードを使用します。 これは、PNP Irp を処理するときに頻繁に実行されます。 たとえば、受信、 [IRP_MN_START_DEVICE](irp-mn-start-device.md) IRP、バス ドライバーに IRP を転送し、デバイスを開始する前に完了するまで待機します。 呼び出すことができます[ **IoForwardIrpSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff549100)を簡単にこの操作を実行します。

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

### <a name="scenario-3-forward-with-a-completion-routine"></a>例 3:完了ルーチンを転送します。

この場合、ドライバーは完了ルーチンの設定、IRP を転送が下位のドライバーの状態を返します。 設定完了ルーチンの目的は、戻る途中で IRP のコンテンツを変更します。 

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

場合は、ディスパッチ ルーチンから下位のドライバーの状態が返されます。

* 完了ルーチンの IRP の状態を変更する必要がありますできません。 これは、(Irp が IoStatus.Status を ->) の IRP IoStatus ブロックで設定された状態値が下位のドライバーの戻り値の状態と同じであることを確認します。
* Irp が示すとおり、IRP の保留中の状態を反映する必要があります PendingReturned]-> [です。
* IRP の同期を変更する必要がありません。

その結果、(31 および 32) は、このシナリオでは完了ルーチンの 2 つの有効なバージョンはのみです。

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

### <a name="scenario-4-queue-for-later-or-forward-and-reuse"></a>シナリオ 4:後で、キューまたは転送して再利用

キュー IRP いると後で処理または下位のドライバーに IRP を転送して特定の IRP が完了するまでの時間数で再利用するドライバーが必要があるような状況では、次のコード スニペットを使用します。 ディスパッチ ルーチンは、保留中の IRP をマークし、IRP が別のスレッドに後で完了するために STATUS_PENDING を返します。 ここでは、完了のルーチンは、(前のシナリオでは) とは異なり、必要に応じて、IRP の状態を変更できます。 

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

STATUS_CONTINUE_COMPLETION または STATUS_MORE_PROCESSING_REQUIRED 完了ルーチンを返すか、できます。 別のスレッドから IRP を再利用し、後で入力する場合にのみ、STATUS_MORE_PROCESSING_REQUIRED を返します。

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

### <a name="scenario-5-complete-the-irp-in-the-dispatch-routine"></a>シナリオ 5:ディスパッチ ルーチンで IRP を完了します。

このシナリオでは、ディスパッチ ルーチンで IRP を完了する方法を示します。 

**重要な**ディスパッチ ルーチンでは IRP を完了するとディスパッチ ルーチンの戻り値の状態が IRP の IoStatus ブロックで設定されている値の状態に一致する必要があります (Irp が IoStatus.Status を ->)。

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

## <a name="creating-irps-and-sending-them-to-another-driver"></a>Irp を作成して、別のドライバーに送信

### <a name="introduction"></a>概要

シナリオを検証する前に、同期入力/出力要求のドライバーが作成したパケット (IRP) と非同期の要求の違いを理解する必要があります。 

|    同期 (スレッド) の IRP                                                                                                                        |    非同期 (非スレッド) の IRP                                                                                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    IoBuildSynchronousFsdRequest または IoBuildDeviceIoControlRequest を使用して作成されます。                                                                  |    IoBuildAsynchronousFsdRequest または IoAllocateIrp を使用して作成されます。 これは、ドライバーの通信用。                                 |
|    スレッドは IRP が完了するまで待つ必要があります。                                                                                                         |    スレッドは IRP が完了するまで待機する必要はありません。                                                                                                 |
|    作成したスレッドに関連付けられた、そのため、スレッド Irp という名前です。 そのため、スレッドが終了すると、I/O マネージャーは IRP をキャンセルします。     |    作成したスレッドに関連付けられていません。                                                                                                       |
|    任意のスレッド コンテキストで作成できません。                                                                                                 |    スレッドは IRP が完了するまで待たないために、任意のスレッド コンテキストで作成できます。                                             |
|    I/O マネージャーは IRP に関連付けられているバッファーを解放するための完了後です。                                                     |    I/O マネージャーは、クリーンアップを行うことはできません。 ドライバーは、完了ルーチンを提供し、IRP に関連付けられているバッファーを解放する必要があります。          |
|    PASSIVE_LEVEL 等しく IRQL レベルで送信する必要があります。                                                                                                |    IRQL で送信できる以下 DISPATCH_LEVEL ターゲット ドライバーのディスパッチ ルーチンは DISPATCH_LEVEL で要求を処理できる場合にします。     |

### <a name="scenario-6-send-a-synchronous-device-control-request-irpmjinternaldevicecontrolirpmjdevicecontrol-by-using-iobuilddeviceiocontrolrequest"></a>シナリオ 6:IoBuildDeviceIoControlRequest を使用して同期デバイス制御要求 (IRP_MJ_INTERNAL_DEVICE_CONTROL/IRP_MJ_DEVICE_CONTROL) を送信します。

次のコードを呼び出す方法を示します[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)同期 IOCTL 要求に要求します。  詳細については、次を参照してください。 [IRP_MJ_INTERNAL_DEVICE_CONTROL](irp-mj-internal-device-control.md)と[IRP_MJ_DEVICE_CONTROL](irp-mj-device-control.md)します。

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

### <a name="scenario-7-send-a-synchronous-device-control-ioctl-request-and-cancel-it-if-not-completed-in-a-certain-time-period"></a>シナリオ 7:同期デバイス制御 (IOCTL) 要求を送信し、一定時間で完了していない場合は、キャンセル 
このシナリオでは、無期限に待機している要求が完了するため、代わりにユーザーが指定した時間の待機していることを除いては、前のシナリオに似ていますし、待機がタイムアウトした場合に安全に IOCTL 要求を取り消します。 

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

### <a name="scenario-8-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-statuscontinuecompletion"></a>シナリオ 8:IoBuildSynchronousFsdRequest を使用して、IOCTL 以外の同期要求を送信する-完了ルーチンが STATUS_CONTINUE_COMPLETION を返します
次のコードは、呼び出すことによって、IOCTL 以外の同期要求を作成する方法を示しています。 [ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)します。 ここで示す手法は、シナリオ 6 に似ています。

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

### <a name="scenario-9-send-a-synchronous-non-ioctl-request-by-using-iobuildsynchronousfsdrequest---completion-routine-returns-statusmoreprocessingrequired"></a>シナリオ 9:IoBuildSynchronousFsdRequest を使用して、IOCTL 以外の同期要求を送信する-完了ルーチンが STATUS_MORE_PROCESSING_REQUIRED を返します 
このシナリオと 8 のシナリオの唯一の違いは、完了ルーチンが STATUS_MORE_PROCESSING_REQUIRED を返します。 

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

### <a name="scenario-10-send-an-asynchronous-request-by-using-iobuildasynchronousfsdrequest"></a>シナリオ 10:IoBuildAsynchronousFsdRequest を使用して非同期要求を送信します。 
このシナリオは、呼び出すことによって、非同期要求を作成する方法を示しています。 [ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)します。 

非同期の要求で要求を作成したスレッドは IRP が完了するまで待機するがありません。 IRP がスレッドに関連付けられていないために、IRP を任意のスレッド コンテキストで作成できます。 完了ルーチンを提供し、IRP を再利用する予定がない場合に、完了ルーチンのバッファーと IRP をリリースする必要があります。 これは I/O マネージャーがドライバーを作成する非同期 Irp の完了後のクリーンアップを実行できないためです (で作成された**IoBuildAsynchronousFsdRequest**と**IoAllocateIrp**)。 

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

### <a name="scenario-11-send-an-asynchronous-request-by-using-ioallocateirp"></a>シナリオ 11:IoAllocateIrp を使用して非同期要求を送信します。

このシナリオは、呼び出す代わりに点を除いて前のシナリオに似ています[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)、このシナリオでは、 [ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257) IRP を作成する関数。

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

### <a name="scenario-12-send-an-asynchronous-request-and-cancel-it-in-a-different-thread"></a>シナリオ 12:非同期要求を送信し、別のスレッドでキャンセルします。 
このシナリオは、送信する方法 1 つの要求時に、下位のドライバーに完了するには、要求を待つことがなくを表示し、別のスレッドから、いつでも、要求をキャンセルすることもできます。 

デバイスの拡張機能またはデバイスを次に示すようにグローバル context 構造は、この作業を行うには、IRP とその他の変数を覚えてことができます。 IRP の状態は、デバイスの拡張機能で IRPLOCK 変数で追跡されます。 IrpEvent を使用している IRP が完全に完了 (または解放)、次の要求を行う前にかどうかを確認します。 

このイベントは、処理する際にも役立ちます[IRP_MN_REMOVE_DEVICE](irp-mn-remove-device.md)と[IRP_MN_STOP_DEVICE PNP](irp-mn-stop-device.md)がない保留中の Irp これらの要求を完了する前に確認するに要求します。 このイベントは、同期イベント AddDevice またはその他の初期化ルーチンとして初期化するときに最適です。

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

## <a name="references"></a>参考資料 
* Walter Oney します。 Windows Driver Model、第 2 版、第 5 章をプログラミングします。
