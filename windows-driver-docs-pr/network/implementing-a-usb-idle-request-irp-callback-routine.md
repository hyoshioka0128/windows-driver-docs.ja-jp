---
title: USB アイドル要求 IRP コールバック ルーチンの実装
description: USB アイドル要求 IRP コールバック ルーチンの実装
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3e4575f069e878f9b905ce9d6725c44a87db9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843438"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>USB アイドル要求 IRP コールバック ルーチンの実装


[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)が呼び出されると、usb ミニポートドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、usb アイドル\_要求に対して I/O 要求パケット (IRP) を発行します。これは、基になる usb バスドライバーに[ **\_アイドル\_通知を送信\_ための、内部\_usb を送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)します。 ミニポートドライバーは、ネットワークアダプターがアイドル状態で、中断する必要があることを USB バスドライバーに通知するために、この IRP を発行します。

USB ミニポートドライバーは、USB アイドル要求の IRP に対する IRP コールバックルーチンを提供する必要があります。 USB バスドライバーは、ネットワークアダプターを中断して低電力状態に移行できると判断したときに、このルーチンを呼び出します。

**注**  usb バスドライバーが usb アイドル要求の IRP を処理した後、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)への呼び出しのコンテキストでコールバックルーチンを同期的に呼び出すか、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)がを返すと非同期的に呼び出します。

 

コールバックルーチンは、ネットワークアダプターの省電力状態の移行を続行できることを NDIS に通知するために、 [**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出す必要があります。 ドライバーが**NdisMIdleNotificationConfirm**を呼び出す場合は、ネットワークアダプターの移行先として使用できるデバイスの電源の最小状態も指定する必要があります。

[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)の呼び出しのコンテキスト内で、NDIS はネットワークアダプターを低電力状態に移行するために必要な手順を実行します。 詳細については、「 [NDIS の選択的中断のアイドル通知を処理する](handling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

次に、USB アイドル要求の IRP のコールバックルーチンの例を示します。

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

USB アイドル要求のコールバックルーチンの詳細については、「USB アイドル要求の IRP コールバックルーチン」を参照してください。

 

 





