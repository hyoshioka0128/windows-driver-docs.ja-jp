---
title: MiniportIdleNotification ハンドラー関数の実装
description: MiniportIdleNotification ハンドラー関数の実装
ms.assetid: F2F8C98F-D8B3-49A6-819D-BC0EC936F41E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d3fb7e273094f3f7c6d89834c52d30ebe58796d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580365"
---
# <a name="implementing-a-miniportidlenotification-handler-function"></a>MiniportIdleNotification ハンドラー関数の実装


NDIS ミニポート ドライバーの呼び出す[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)選択的にネットワーク アダプターを中断するためにハンドラー関数。 NDIS アダプターは、低電力状態を遷移するときに、アダプターが中断されます。

ネットワーク アダプターがまだ使用されている場合、ミニポート ドライバーがアイドル状態の通知を拒否することができます。 NDIS を返すことによってこのドライバーでは\_状態\_から時間、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数。

**注**  ミニポート ドライバーはアイドル状態の通知を拒否できない場合、 *ForceIdle*のパラメーター、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数に設定されている**TRUE**します。

 

ミニポート ドライバーがアイドル状態の通知を拒否しては場合は、基になるバス ドライバーをバスに固有の I/O 要求パケット (Irp) を発行する必要があります。 これらの Irp では、アダプターのアイドル状態と、アダプターは、低電力状態に移行することを確認する要求について、バス ドライバーに通知します。

たとえば、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)を呼び出すと、USB ミニポート ドライバーは、USB アイドル状態の要求の I/O 要求パケット (IRP) を準備します ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270))。 、ミニポート ドライバーが IRP を準備するとき、コールバック関数を指定する必要があります。 ドライバーでは、呼び出す必要がありますも[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)または[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)完了ルーチンを指定するにはIRP します。 ミニポート ドライバーを呼び出して[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) USB バス ドライバーに IRP を発行します。

**注**  USB バス ドライバーが IRP をすぐに完了しません。 IRP が低電力の移行を保留中状態のままにします。 ミニポート ドライバーによって取り消されるか、USB ハブからのネットワーク アダプターの突然の削除などのハードウェア イベントが発生した場合にのみ、バス ドライバーは IRP を完了します。

 

例を次に、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092) USB ミニポート ドライバーのハンドラー関数。 この例では、基になる USB ドライバーを USB アイドル状態の要求 IRP の発行に関連する手順を示します。 この例も示す方法で以前に割り当てられた IRP のリソース[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)IRP の再利用できます。

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

USB アイドル要求 IRP のコールバック ルーチンの実装のガイドラインについては、次を参照してください。 [USB のアイドル状態要求 IRP のコールバック ルーチンを実装する](implementing-a-usb-idle-request-irp-callback-routine.md)します。

 

 





