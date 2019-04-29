---
Description: このトピックでは、USB ドライバー スタックに特定の要求を処理するのに初期化された URB を送信するために必要な手順について説明します。
title: URB の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ada89a24eddfc269748427e0276e129799269a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331072"
---
# <a name="how-to-submit-an-urb"></a>URB の送信方法


このトピックでは、USB ドライバー スタックに特定の要求を処理するのに初期化された URB を送信するために必要な手順について説明します。

クライアント ドライバーは、型の I/O 要求パケット (Irp) のデバイスに配信される I/O 制御コード (IOCTL) 要求を使用して、そのデバイスと通信する[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)します。 など、選択構成要求をデバイス固有の要求の要求で、USB 要求ブロック (URB) に関連付けられた IRP を説明します。 IRP、URB を関連付けると、USB ドライバー スタックに要求を送信するプロセスを URB の送信と呼びます。 クライアント ドライバーを使用する必要があります、URB を送信する[ **IOCTL\_内部\_USB\_送信\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271)デバイス制御コードとします。 IOCTL では、クライアント ドライバーを使用して、デバイスが接続されているポートとそのデバイスを管理する I/O インターフェイスを提供する「内部」の制御コードの 1 つです。 ユーザー モード アプリケーションには、その内部の I/O インターフェイスにアクセスがありません。 カーネル モード ドライバーの詳細の制御コードを参照してください。 [USB クライアント ドライバーのカーネル モードの Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#km-ioctl)します。

### <a name="prerequisites"></a>前提条件

ユニバーサル シリアル バス (USB) ドライバー スタックに要求を送信する前に、クライアント ドライバーを割り当てる必要があります、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体し、要求の種類によっては、その構造の書式を設定します。 詳細については、次を参照してください。[割り当てと構成の翻訳](how-to-add-xrb-support-for-client-drivers.md)と[ベスト プラクティス。翻訳を使用して](usb-client-driver-contract-in-windows-8.md)します。

<a name="instructions"></a>手順
------------

1.  URB を呼び出すことによって、IRP を割り当て、 [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)ルーチン。 IRP を受信するデバイス オブジェクトのスタック サイズを指定する必要があります。 以前の呼び出しでそのデバイス オブジェクトへのポインターを受け取った、 [ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)ルーチン。 スタック サイズが格納されている、 **StackSize**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。
2.  IRP の最初のスタックの場所へのポインターを取得 ([**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)) を呼び出して[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266).
3.  設定、 **MajorFunction**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体を[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)します。
4.  設定、 **Parameters.DeviceIoControl.IoControlCode**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体を[**IOCTL\_内部\_USB\_送信\_URB**](https://msdn.microsoft.com/library/windows/hardware/ff537271)します。
5.  設定、 **Parameters.Others.Argument1**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)初期化のアドレスに構造体[**URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。 IRP URB を関連付けるを呼び出すことができますまた[ **USBD\_AssignUrbToIoStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/hh406228) URB がによって割り当てられた場合にのみ[ **USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)、 [ **USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)、または[ **USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)します。
6.  完了ルーチンを呼び出すことによって設定[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)します。

    URB を非同期的に送信する場合、呼び出し元実装完了ルーチンとそのコンテキストへのポインターを渡します。 呼び出し元は、その完了ルーチンの IRP を解放します。

    IRP を同期的に送信する場合は、完了ルーチンを実装してへの呼び出しでは、そのルーチンへのポインターを渡す[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)します。 呼び出しでは、初期化された KEVENT オブジェクトも必要です、*コンテキスト*パラメーター。 完了ルーチンのイベントをシグナル状態に設定します。

7.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)デバイス スタックの次のような低いデバイス オブジェクトに設定されている IRP を転送します。 呼び出した後、同期呼び出しの**保留**、呼び出すことによって、イベント オブジェクトの待機[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)イベント通知を取得します。
8.  IRP の完了したら、チェック、 **IoStatus.Status** IRP のメンバーと、結果を評価します。 場合、 **IoStatus.Status**ステータス\_成功すると、要求が成功します。

## <a name="complete-example"></a>完全な例


次の例では、同期的に、URB を送信する方法を示します。

```ManagedCPlusPlus
// The SubmitUrbSync routine submits an URB synchronously.
//
// Parameters:
//      DeviceExtension: Pointer to the caller's device extension. The
//                       device extension must have a pointer to 
//                       the next lower device object in the device stacks.  
//
//      Irp: Pointer to an IRP allocated by the caller.
//
//      Urb: Pointer to an URB that is allocated by  USBD_UrbAllocate, 
//           USBD_IsochUrbAllocate, USBD_SelectConfigUrbAllocateAndBuild, 
//           or USBD_SelectInterfaceUrbAllocateAndBuild.

//      CompletionRoutine: Completion routine.
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS  

NTSTATUS SubmitUrbSync( PDEVICE_EXTENSION DeviceExtension,
                       PIRP Irp,
                       PURB Urb,  
                       PIO_COMPLETION_ROUTINE SyncCompletionRoutine)  

{

    NTSTATUS  ntStatus;  
    KEVENT    kEvent;

    PIO_STACK_LOCATION nextStack;

    // Get the next stack location.
    nextStack = IoGetNextIrpStackLocation(Irp);  

    // Set the major code.
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    // Set the IOCTL code for URB submission.
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    // Attach the URB to this IRP.
    // The URB must be allocated by USBD_UrbAllocate, USBD_IsochUrbAllocate, 
    // USBD_SelectConfigUrbAllocateAndBuild, or USBD_SelectInterfaceUrbAllocateAndBuild.
    USBD_AssignUrbToIoStackLocation (DeviceExtension->UsbdHandle, nextStack, Urb);

    KeInitializeEvent(&kEvent, NotificationEvent, FALSE);

    ntStatus = IoSetCompletionRoutineEx ( DeviceExtension->NextDeviceObject,  
        Irp,  
        SyncCompletionRoutine,  
        (PVOID) &kEvent,  
        TRUE, 
        TRUE, 
        TRUE);

    if (!NT_SUCCESS(ntStatus))
    {
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "IoSetCompletionRoutineEx failed. \n" ));
        goto Exit;
    }

    ntStatus = IoCallDriver(DeviceExtension->NextDeviceObject, Irp);  

    if (ntStatus == STATUS_PENDING) 
    {
        KeWaitForSingleObject ( &kEvent,
            Executive,
            KernelMode,
            FALSE,
            NULL);
    }

    ntStatus = Irp->IoStatus.Status;

Exit:

    if (!NT_SUCCESS(ntStatus))
    {
        // We hit a failure condition, 
        // We will free the IRP

        IoFreeIrp(Irp);
        Irp = NULL;
    }


    return ntStatus;
}

// The SyncCompletionRoutine routine is the completion routine 
// for the synchronous URB submit request.          
//
// Parameters:
//
//      DeviceObject: Pointer to the device object. 
//      Irp:          Pointer to an I/O Request Packet. 
//      CompletionContext: Context for the completion routine.
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS  

NTSTATUS SyncCompletionRoutine ( PDEVICE_OBJECT DeviceObject,
                                PIRP           Irp,
                                PVOID          Context)
{
    PKEVENT kevent;

    kevent = (PKEVENT) Context;

    if (Irp->PendingReturned == TRUE)
    {
        KeSetEvent(kevent, IO_NO_INCREMENT, FALSE);
    }

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "Request completed. \n" ));


    return STATUS_MORE_PROCESSING_REQUIRED;
} 
```

## <a name="complete-example"></a>完全な例


次の例では、URB を非同期的に送信する方法を示します。

```ManagedCPlusPlus
// The SubmitUrbASync routine submits an URB asynchronously.
//
// Parameters:
//
// Parameters:
//      DeviceExtension: Pointer to the caller's device extension. The
//                       device extension must have a pointer to 
//                       the next lower device object in the device stacks.  
//
//      Irp: Pointer to an IRP allocated by the caller.
//
//      Urb: Pointer to an URB that is allocated by  USBD_UrbAllocate, 
//           USBD_IsochUrbAllocate, USBD_SelectConfigUrbAllocateAndBuild, 
//           or USBD_SelectInterfaceUrbAllocateAndBuild.

//      CompletionRoutine: Completion routine.
//
//      CompletionContext: Context for the completion routine.
//
//
// Return Value:                                                       
//                                                                      
//      NTSTATUS      

NTSTATUS SubmitUrbASync ( PDEVICE_EXTENSION DeviceExtension,
                         PIRP Irp,
                         PURB Urb,  
                         PIO_COMPLETION_ROUTINE CompletionRoutine,  
                         PVOID CompletionContext)  
{
    // Completion routine is required if the URB is submitted asynchronously.
    // The caller's completion routine releases the IRP when it completes.


    NTSTATUS ntStatus = -1;  

    PIO_STACK_LOCATION nextStack = IoGetNextIrpStackLocation(Irp);  

    // Attach the URB to this IRP.
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;  

    // Attach the URB to this IRP.
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;  

    // Attach the URB to this IRP.
    (void) USBD_AssignUrbToIoStackLocation (DeviceExtension->UsbdHandle, nextStack, Urb);  

    // Caller's completion routine will free the irp when it completes.
    ntStatus = IoSetCompletionRoutineEx ( DeviceExtension->NextDeviceObject,
        Irp,  
        CompletionRoutine,  
        CompletionContext,  
        TRUE, 
        TRUE, 
        TRUE);

    if (!NT_SUCCESS(ntStatus))
    {
        goto Exit;
    }

    (void) IoCallDriver(DeviceExtension->NextDeviceObject, Irp);

Exit:
    if (!NT_SUCCESS(ntStatus))
    {
        // We hit a failure condition, 
        // We will free the IRP

        IoFreeIrp(Irp);
        Irp = NULL;
    }

    return ntStatus;
}
```

## <a name="related-topics"></a>関連トピック
[USB デバイスに要求を送信](communicating-with-a-usb-device.md)  



