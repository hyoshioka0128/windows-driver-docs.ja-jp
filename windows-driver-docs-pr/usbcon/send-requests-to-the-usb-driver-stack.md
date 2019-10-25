---
Description: このトピックでは、初期化された URB を USB ドライバースタックに送信して特定の要求を処理するために必要な手順について説明します。
title: URB の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fb7c2948c0bf0656bc09df5286da2f0b81b8315
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824162"
---
# <a name="how-to-submit-an-urb"></a>URB の送信方法


このトピックでは、初期化された URB を USB ドライバースタックに送信して特定の要求を処理するために必要な手順について説明します。

クライアントドライバーは、デバイスに送信される i/o 制御コード (IOCTL) 要求を使用して、デバイスと通信します。 i/o 要求パケット (Irp) は、[**内部\_デバイス\_制御\_、MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)型の i/o 要求パケット (irp) を使用します。 選択構成要求などのデバイス固有の要求の場合、要求は、IRP に関連付けられている USB 要求ブロック (URB) で記述されます。 URB を IRP に関連付けて、USB ドライバースタックに要求を送信するプロセスは、URB の送信と呼ばれます。 URB を送信するには、クライアントドライバーが[**IOCTL\_内蔵\_USB\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)デバイス制御コードとして\_URB を送信する必要があります。 IOCTL は、クライアントドライバーがデバイスを管理するために使用する i/o インターフェイスと、デバイスが接続されているポートを提供する "内部" 制御コードの1つです。 ユーザーモードのアプリケーションは、これらの内部 i/o インターフェイスにアクセスすることはできません。 カーネルモードドライバーの制御コードの詳細については、「 [USB クライアントドライバーのカーネルモード ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#km-ioctl)」を参照してください。

### <a name="prerequisites"></a>前提条件

USB (Universal Serial Bus) ドライバースタックに要求を送信する前に、クライアントドライバーは、要求の種類に応じて、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当て、その構造をフォーマットする必要があります。 詳細については、「 [URBs の割り当てとビルド](how-to-add-xrb-support-for-client-drivers.md)」と「[ベストプラクティス: URBs を使用する](usb-client-driver-contract-in-windows-8.md)」を参照してください。

<a name="instructions"></a>手順
------------

1.  [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)ルーチンを呼び出して、URB に IRP を割り当てます。 IRP を受信するデバイスオブジェクトのスタックサイズを指定する必要があります。 [**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)ルーチンを以前に呼び出したときに、そのデバイスオブジェクトへのポインターを受け取りました。 スタックサイズは、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**StackSize**メンバーに格納されます。
2.  [**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出すことにより、IRP の最初のスタック位置 ([**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) へのポインターを取得します。
3.  [**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**MajorFunction**メンバーを[**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に設定します。
4.  [**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**Parameters. DeviceIoControl のコード**メンバーを[**IOCTL\_内部\_USB\_送信\_URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)に設定します。
5.  [**IO\_\_スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の**引数 1**メンバーを、初期化された[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体のアドレスに設定します。 IRP を URB に関連付けるには、 [**USBD\_割り当て Urbtoiostacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)を呼び出すことができます。 USBD によって割り当てられたのが[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)、 [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)、または USBD である場合のみ[ **\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)。
6.  [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)を呼び出して、完了ルーチンを設定します。

    URB を非同期に送信する場合は、呼び出し元によって実装された完了ルーチンとそのコンテキストへのポインターを渡します。 呼び出し元は、完了ルーチンで IRP を解放します。

    IRP を同期的に送信する場合は、完了ルーチンを実装し、 [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)への呼び出しでそのルーチンへのポインターを渡します。 この呼び出しでは、*コンテキスト*パラメーターに初期化された KEVENT オブジェクトも必要です。 完了ルーチンで、イベントをシグナル状態に設定します。

7.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、設定された IRP をデバイススタック内の次に小さいデバイスオブジェクトに転送します。 同期呼び出しの場合は、 **IoCallDriver**を呼び出した後、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出してイベント通知を取得することによって、イベントオブジェクトを待機します。
8.  IRP の完了後に、IRP の**iostatus. Status**メンバーを確認し、結果を評価します。 **Iostatus**が STATUS\_SUCCESS の場合、要求は成功しました。

## <a name="complete-example"></a>完全な例


次の例は、URB を同期的に送信する方法を示しています。

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


次の例は、URB を非同期に送信する方法を示しています。

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
[USB デバイスへの要求の送信](communicating-with-a-usb-device.md)  



