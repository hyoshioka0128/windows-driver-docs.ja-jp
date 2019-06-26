---
title: NDIS セレクティブ サスペンドの IRP リソースの管理
description: NDIS セレクティブ サスペンドの IRP リソースの管理
ms.assetid: 542A96A7-AD6D-4780-8FEF-34730A663C1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3958b35086b5d884e13a9b8b3776cc9ea5bba5f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356165"
---
# <a name="managing-irp-resources-for-ndis-selective-suspend"></a>NDIS セレクティブ サスペンドの IRP リソースの管理


ミニポート ドライバーがサポートされ、選択的 NDIS、可能である場合の中断、NDIS 呼び出し[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)ネットワーク アダプターが非アクティブになった場合、ドライバーをアイドル状態の通知を発行します。 ミニポート ドライバーでは、この通知を処理する場合は、I/O 要求パケット (Irp) を基になるバス ドライバーに発行する必要があります。 これらの Irp では、アダプターのアイドル状態と、アダプターは、低電力状態に移行することを確認する要求について、バス ドライバーに通知します。

ミニポート ドライバーで発行される Irp では、bus 固有です。 たとえば、NDIS を呼び出すと[ *MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)、USB ミニポート USB アイドル状態の要求を発行する ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP を基になる USB バス ドライバー。

NDIS は、可能性があります、アイドル状態の通知を発行、ミニポート ドライバー何度も、ドライバーが初期化された後します。 ドライバーがドライバーへの呼び出しのコンテキストで USB アイドル要求 IRP のリソースを割り当てること勧めそのため、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

次の例では、ミニポート ドライバーが IRP のリソースを割り当てる方法を示します。

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

呼び出し中に、ミニポート ドライバーが IRP リソースを割り当てますかどうか[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)、ドライバーが呼び出し中にこれらのリソースを解放する必要があります[ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)します。

次の例では、ミニポート ドライバーが IRP のリソースを解放する方法を示します。

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
