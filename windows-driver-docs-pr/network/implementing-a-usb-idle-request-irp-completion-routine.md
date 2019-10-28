---
title: USB アイドル要求 IRP 完了ルーチンの実装
description: USB アイドル要求 IRP 完了ルーチンの実装
ms.assetid: C9435A1D-031B-4F67-B968-66534C48A9BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea207a38ce128668b61cdc9bdbd3d16c084fcbca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843436"
---
# <a name="implementing-a-usb-idle-request-irp-completion-routine"></a>USB アイドル要求 IRP 完了ルーチンの実装


[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)が呼び出されると、usb ミニポートドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、usb アイドル要求に対して I/O 要求パケット (IRP) を発行します ([**IOCTL\_内部\_usb\_送信\_アイドル状態\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を基になる USB バスドライバーに通知します。 ミニポートドライバーは、ネットワークアダプターがアイドル状態で、中断する必要があることを USB バスドライバーに通知するために、この IRP を発行します。

Usb ミニポートドライバーは、USB アイドル要求の IRP に対して完了ルーチンを登録するために、 [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)を呼び出す必要もあります。 Usb バスドライバーは、USB ミニポートドライバーによってキャンセルされた後に IRP が完了すると、完了ルーチンを呼び出します。 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)を呼び出すことによって、NDIS がアイドル通知をキャンセルすると、USB ミニポートドライバーは IRP をキャンセルします。

完了ルーチンは、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出して、ネットワークアダプターのフルパワー状態の移行を続行できることを NDIS に通知するためにのみ必要です。

  完了ルーチンは、NDIS からの別のアイドル通知中に、USB ミニポートドライバーが IRP リソースを再利用する場合に必要な\_\_の\_の状態を返す必要がある**ことに注意**してください。

 

次に、USB アイドル要求の IRP の完了ルーチンの例を示します。

```C++
//
// MiniportUsbIdleRequestCompletion()
//
// This is the IO_COMPLETION_ROUTINE for the selective suspend IOCTL.
// All that is needed is to inform NDIS that the IdleNotification
// operation is complete.
//
VOID MiniportUsbIdleRequestCompletion(PVOID AdapterContext)
{
    NdisMIdleNotificationComplete(Adapter->MiniportAdapterHandle);

    // We will be reusing the IRP later, so do not let the IO manager delete it.
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

USB アイドル要求のコールバックルーチンの詳細については、「USB アイドル要求の IRP 完了ルーチン」を参照してください。

 

 





