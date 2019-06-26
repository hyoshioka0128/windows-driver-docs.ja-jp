---
title: USB アイドル要求 IRP コールバック ルーチンの実装
description: USB アイドル要求 IRP コールバック ルーチンの実装
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be55e45fb984ac53b29cec8048bd694172e45394
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382669"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>USB アイドル要求 IRP コールバック ルーチンの実装


ときに[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)を呼び出すと、USB のミニポート ドライバー呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) I/O 要求パケット (IRP) を発行するにはUSB のアイドル状態の要求 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) に、基になる USB バス ドライバー。 ミニポート ドライバーでは、ネットワーク アダプターがアイドル状態し、中断する必要があります、USB バス ドライバーに通知するには、この IRP を発行します。

USB ミニポート ドライバーでは、USB アイドル要求 IRP の IRP のコールバック ルーチンを提供する必要があります。 USB バス ドライバーは、ネットワーク アダプターの中断し、低電力状態に移行することを確認するときに、このルーチンを呼び出します。

**注**  後に、USB バス ドライバーが IRP USB アイドル状態要求を処理、いずれかへの呼び出しのコンテキストで同期的に、コールバック ルーチンを呼び出します[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)または後で非同期的に[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)を返します。

 

呼び出すコールバック ルーチンがしか[ **NdisMIdleNotificationConfirm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)ネットワーク アダプターの省電力状態の遷移を続行できる NDIS を通知するためにします。 ドライバーを呼び出すと**NdisMIdleNotificationConfirm**、ネットワーク アダプターに移行できる、最も低いデバイスの電源状態も指定する必要があります。

呼び出しのコンテキスト内で[ **NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)NDIS 低電力状態にネットワーク アダプターに移行するために必要な手順を実行します。 詳細については、次を参照してください。 [、NDIS セレクティブ サスペンド アイドル状態の通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)します。

次は、USB アイドル要求 IRP のコールバック ルーチンの例です。

```C++
//
// MiniportUsbIdleRequestCallback()
//
// This is the USB selective suspend idle notification.  All that is 
// needed is to inform NDIS that the USB stack is ready to go to a 
// low-power state.  Be aware that USB devices will always be requested
// to transition to a power state of NdisDeviceStateD2.
//
VOID MiniportUsbIdleRequestCallback(PVOID AdapterContext)
{
    NdisMIdleNotificationConfirm(
        AdapterContext->MiniportAdapterHandle,
        NdisDeviceStateD2
        );

    return;
}
```

USB のアイドル状態の要求のコールバック ルーチンの詳細については、USB アイドル要求 IRP のコールバック ルーチンを参照してください。

 

 





