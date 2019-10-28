---
title: MiniportCancelIdleNotification ハンドラー関数の実装
description: MiniportCancelIdleNotification ハンドラー関数の実装
ms.assetid: 51C25573-5723-44F9-B498-EBEF6756F3B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42f02596da40ba369da896ce4ce0cbcc4845ef25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843441"
---
# <a name="implementing-a-miniportcancelidlenotification-handler-function"></a>MiniportCancelIdleNotification ハンドラー関数の実装


NDIS は、アイドル通知プロセスをキャンセルし、ネットワークアダプターをフルパワー状態に移行するために、ミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出します。 この関数が呼び出されると、ミニポートドライバーは次の手順に従う必要があります。

1.  ミニポートドライバーは、アイドル通知に対して以前に発行された可能性があるすべてのバス固有の Irp をキャンセルする必要があります。

2.  ミニポートドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。 この呼び出しは、アイドル状態の通知が完了したことを NDIS に通知します。 その後、NDIS はネットワークアダプターをフルパワー状態に移行することによって、セレクティブサスペンド操作を複雑します。

たとえば、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)が呼び出されると、usb ミニポートドライバーは[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出して、usb アイドル要求の I/O 要求パケット (IRP) をキャンセルします ([**IOCTL\_内部\_usb\_送信\_アイドル状態\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification))。 USB ミニポートドライバーは、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数でこの IRP を以前に発行しました。 USB バスドライバーは、IRP をキャンセルするとすぐに、IRP の完了ルーチンを呼び出します。 USB バスドライバーは、完了ルーチンを呼び出すと、IRP が取り消されたことを確認し、デバイスをフルパワー状態に再開できることを確認します。 完了ルーチンのコンテキストでは、ミニポートドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。

USB バスドライバーは、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)の呼び出しのコンテキスト内で、または[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)が返された後に非同期的に完了ルーチンを呼び**出すことができる  ます**。

 

次に、USB ミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数の例を示します。 この例は、USB アイドル要求 IRP のキャンセルに関連する手順を示しています。

```C++
//
// MiniportCancelIdleNotification()
//
// This routine is called if NDIS has to cancel an idle notification.
// All that is needed is to cancel the selective suspend IRP.
//
VOID MiniportCancelIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext
    )
{
    IoCancelIrp(Adapter->UsbSsIrp);
}
```

USB アイドル要求 IRP の完了ルーチンの実装に関するガイドラインについては、「 [Usb アイドル要求の Irp 完了ルーチンの実装](implementing-a-usb-idle-request-irp-completion-routine.md)」を参照してください。

 

 





