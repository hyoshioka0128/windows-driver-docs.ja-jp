---
title: MiniportIdleNotification ハンドラー関数の実装
description: MiniportIdleNotification ハンドラー関数の実装
ms.assetid: F2F8C98F-D8B3-49A6-819D-BC0EC936F41E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe85f744696038eba9f94d782445f2b3f9fce084
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843439"
---
# <a name="implementing-a-miniportidlenotification-handler-function"></a>MiniportIdleNotification ハンドラー関数の実装


NDIS は、ネットワークアダプターを選択的に中断するために、ミニポートドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出します。 NDIS がアダプターを低電力状態に移行すると、アダプターは中断されます。

ネットワークアダプターがまだ使用されている場合、ミニポートドライバーはアイドル状態の通知を拒否することがあります。 ドライバーは、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数から NDIS\_STATUS\_BUSY を返すことによってこれを行います。

[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数の*ForceIdle*パラメーターが**TRUE**に設定されている場合、ミニポートドライバーはアイドル状態の通知を拒否できない  に**注意**してください。

 

ミニポートドライバーがアイドル状態の通知を拒否しない場合、基盤となるバスドライバーにバス固有の i/o 要求パケット (Irp) を発行することが必要になる場合があります。 これらの Irp は、アダプターのアイドル状態についてバスドライバーに通知し、アダプターが低電力状態に移行できることを確認するように要求します。

たとえば、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)が呼び出されると、usb ミニポートドライバーは、usb アイドル要求に対して i/o 要求パケット (IRP) を準備します ([**IOCTL\_内部\_usb\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification))。 ミニポートドライバーは、IRP を準備するときに、コールバック関数を指定する必要があります。 また、ドライバーは、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)または[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)を呼び出して、IRP の完了ルーチンを指定する必要があります。 次に、ミニポートドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IRP を USB バスドライバーに発行します。

USB バスドライバー  IRP はすぐに完了しない**ことに注意**してください。 IRP は、低電力の移行によって保留中の状態のままになります。 バスドライバーは、ミニポートドライバーによって取り消された場合、またはハードウェアイベントが発生した場合にのみ、IRP を完了します。たとえば、USB ハブからネットワークアダプターが突然削除された場合などです。

 

次に、USB ミニポートドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数の例を示します。 この例では、基になる USB ドライバーへの USB アイドル要求 IRP の発行に関連する手順を示します。 この例では、以前に[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)で割り当てられた irp リソースを irp に再利用できる方法も示しています。

```C++
//
// MiniportIdleNotification()
//
// This routine is invoked by NDIS when it has detected that the miniport
// is idle.  The miniport must prepare to issue its selective suspend IRP
// to the USB stack.  The driver can return NDIS_STATUS_BUSY if it is
// unwilling to become idle at this moment; NDIS will then retry later.
// Otherwise, the miniport should return NDIS_STATUS_PENDING.
//
NDIS_STATUS MiniportIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext,
    _In_ BOOLEAN ForceIdle
    )
{
    PIO_STACK_LOCATION IoSp;

    IoReuseIrp(Adapter->UsbSsIrp, STATUS_NOT_SUPPORTED);

    IoSp = IoGetNextIrpStackLocation(Adapter->UsbSsIrp);
    IoSp->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    IoSp->Parameters.DeviceIoControl.IoControlCode 
            = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    IoSp->Parameters.DeviceIoControl.InputBufferLength 
            = sizeof(Adapter->UsbSsCallback);
    IoSp->Parameters.DeviceIoControl.Type3InputBuffer 
            = Adapter->UsbSsCallback;

    IoSetCompletionRoutine(
            Adapter->UsbSsIrp,
            MiniportUsbIdleRequestCompletion,
            Adapter,
            TRUE,
            TRUE,
            TRUE);

    NtStatus = IoCallDriver(Adapter->Fdo, Adapter->UsbSsIrp);
    if (!NT_SUCCESS(NtStatus))
    {
       return NDIS_STATUS_FAILURE;
    }

    return NDIS_STATUS_PENDING;
}
```

USB アイドル要求 IRP のコールバックルーチンの実装に関するガイドラインについては、「 [Usb アイドル要求の Irp コールバックルーチンの実装](implementing-a-usb-idle-request-irp-callback-routine.md)」を参照してください。

 

 





