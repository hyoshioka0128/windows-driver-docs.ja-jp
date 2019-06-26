---
title: USB アイドル要求 IRP 完了ルーチンの実装
description: USB アイドル要求 IRP 完了ルーチンの実装
ms.assetid: C9435A1D-031B-4F67-B968-66534C48A9BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bfa2fa81066ae977de62ce30662dca643c2aa47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382679"
---
# <a name="implementing-a-usb-idle-request-irp-completion-routine"></a>USB アイドル要求 IRP 完了ルーチンの実装


ときに[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)を呼び出すと、USB のミニポート ドライバー呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) I/O 要求パケット (IRP) を発行するにはUSB のアイドル状態の要求 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) に、基になる USB バス ドライバー。 ミニポート ドライバーでは、ネットワーク アダプターがアイドル状態し、中断する必要があります、USB バス ドライバーに通知するには、この IRP を発行します。

USB のミニポート ドライバーに呼び出す必要がありますも[ **IoSetCompletionRoutineEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex) USB アイドル要求 IRP の完了ルーチンを登録するためにします。 USB バス ドライバーは、USB のミニポート ドライバーによって取り消される後 IRP が完了すると、完了ルーチンを呼び出します。 NDIS は呼び出すことによって、アイドル状態の通知をキャンセルすると、USB のミニポート ドライバーは IRP をキャンセル[ *MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)します。

呼び出して完了ルーチンがしか[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)ネットワーク アダプターの電力状態の遷移を続行できる NDIS を通知するためにします。

**注**  完了ルーチンの状態を返す必要があります\_詳細\_処理\_USB ミニポート ドライバーが IRP のリソースを再利用 NDIS から別のアイドル状態通知中にかどうかに必要な。

 

次は、USB アイドル要求 IRP の完了ルーチンの例です。

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

USB のアイドル状態の要求のコールバック ルーチンの詳細については、USB アイドル要求 IRP の完了ルーチンを参照してください。

 

 





