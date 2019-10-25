---
title: NDIS セレクティブ サスペンドの IRP リソースの管理
description: NDIS セレクティブ サスペンドの IRP リソースの管理
ms.assetid: 542A96A7-AD6D-4780-8FEF-34730A663C1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014594e1bafb69003dde7923f6e8715ba68aa840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844118"
---
# <a name="managing-irp-resources-for-ndis-selective-suspend"></a>NDIS セレクティブ サスペンドの IRP リソースの管理


ミニポートドライバーで NDIS のセレクティブサスペンドがサポートされ、有効になっている場合、NDIS は[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)を呼び出して、ネットワークアダプターが非アクティブになった場合にドライバーへのアイドル通知を発行します。 ミニポートドライバーがこの通知を処理するときに、基になるバスドライバーに i/o 要求パケット (Irp) を発行することが必要になる場合があります。 これらの Irp は、アダプターのアイドル状態についてバスドライバーに通知し、アダプターが低電力状態に移行できることを確認するように要求します。

ミニポートドライバーによって発行される Irp はバス固有です。 たとえば、NDIS が[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)を呼び出すと、usb ミニポートは、基になる usb バスドライバーに、usb アイドル要求[ **\_(内部\_usb\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP を発行します。

NDIS は、ドライバーが初期化された後に、ミニポートドライバーへのアイドル通知を何度も発行する場合があります。 このため、ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数への呼び出しのコンテキストで、USB アイドル要求の IRP のリソースを割り当てることをお勧めします。

次の例は、ミニポートドライバーが IRP リソースを割り当てる方法を示しています。

```C++
//
// MiniportInitializeEx()
//
// In the miniport's initialization routine, the miniport should allocate
// an IRP.  It can also set up the USB_IDLE_CALLBACK_INFO structure that
// will be used with each successive USB idle request.
//
NDIS_STATUS MiniportInitializeEx(
    _In_ NDIS_HANDLE MiniportAdapterHandle,
    _In_ NDIS_HANDLE MiniportDriverContext,
    _In_ PNDIS_MINIPORT_INIT_PARAMETERS MiniportInitParameters
    )
    {
    PIRP UsbSsIrp;
    USB_IDLE_CALLBACK_INFO UsbSsCallback;
    ...

    UsbSsIrp = IoAllocateIrp(Adapter->Fdo->StackSize, FALSE);
    if (!UsbSsIrp)
       {
       // Handle failure
       return NDIS_STATUS_RESOURCES;
       }

    UsbSsCallback.IdleCallback = MiniportUsbIdleRequestCallback;
    UsbSsCallback.IdleContext = Adapter;

    // Save these in the adapter structure for later use
    Adapter->UsbSsIrp = UsbSsIrp;
    Adapter->UsbSsCallback = UsbSsCallback;
    ...
    }
```

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出し中にミニポートドライバーによって IRP リソースが割り当てられた場合、ドライバーは[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)の呼び出し中にこれらのリソースを解放する必要があります。

次の例は、ミニポートドライバーが IRP リソースを解放する方法を示しています。

```C++
//
// MiniportHaltEx
//
// During halt (or when the miniport performs its cleanup from 
// MiniportInitializeEx) the miniport should free the IRP allocated 
// earlier.
//
VOID MiniportHaltEx(
     _In_  NDIS_HANDLE MiniportAdapterContext,
     _In_  NDIS_HALT_ACTION HaltAction
    )
    {
    ...
    if (Adapter->UsbSsIrp)
        {
        IoFreeIrp(Adapter->UsbSsIrp);
        Adapter->UsbSsIrp = NULL;
        }
    ...
    }

```
