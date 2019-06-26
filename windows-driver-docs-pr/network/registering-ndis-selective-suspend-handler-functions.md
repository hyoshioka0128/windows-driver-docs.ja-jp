---
title: NDIS セレクティブ サスペンド ハンドラー関数の登録
description: NDIS セレクティブ サスペンド ハンドラー関数の登録
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5079cb05693596efa5c0e84e1fe9e28eedd41289
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374744"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>NDIS セレクティブ サスペンド ハンドラー関数の登録


ミニポート ドライバーには、選択的 NDIS がサポートしている場合は、中断、NDIS は、基になるネットワーク アダプターがアイドル状態になることをドライバーに通知します。 ミニポート ドライバーでは、これらのアイドル状態の通知を処理するために、次の関数を提供する必要があります。

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)  
NDIS 呼び出し、 [ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)ミニポート ドライバー、ネットワーク アダプターがアイドル状態になることを通知するハンドラー関数。 ミニポート ドライバーは、ネットワーク アダプターが、低電力状態に移行できるかどうかを決定することにより、アイドル状態の通知を処理します。 ミニポート ドライバーでは、バスに固有の方法でこの決定を実行します。

USB のミニポート ドライバーが USB アイドル状態の要求の I/O 要求パケット (IRP) を発行して、ネットワーク アダプターが低電力状態に移行できるかどうかを決定するなど、([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を基になる USB バス ドライバー。 アダプターがアイドル状態し、低電力状態に移行することができます、この IRP の処理、ミニポート ドライバーに通知されます。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)  
NDIS 呼び出し、 [ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)未処理のアイドル状態の通知をキャンセル ハンドラー関数。 この関数が呼び出されると、ミニポート ドライバーは、アイドル状態の通知で以前発行がある可能性があります bus 固有 Irp をキャンセルします。

たとえば、 [ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)を呼び出すと、USB ミニポートが以前に発行された USB アイドル要求 IRP を取り消す必要があります。 IRP が取り消されたときに、アダプターが電力状態に遷移しますようになりましたことができます、ミニポート ドライバーに通知されます。

ときに、ミニポート ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数が呼び出されると、選択的 NDIS は、次の手順に従ってハンドラー関数を中断するドライバー レジスタ。

1.  ミニポート ドライバーを設定する必要があります、 **SetOptionsHandler**のメンバー、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体のドライバーのエントリ ポイントを[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。 ドライバー呼び出し[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)を登録するその**NDIS\_ミニポート\_ドライバー\_特性**NDIS と構造体。

2.  NDIS 呼び出し、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数への呼び出しのコンテキストで[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。

    ときに[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)が呼び出され、ミニポート ドライバーの初期化、 [ **NDIS\_ミニポート\_SS\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_ss_characteristics)ハンドラー関数へのポインターを含む構造体。 ミニポート ドライバーを呼び出して[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)設定と、 *OptionalHandlers*パラメーターへのポインターを**NDIS\_ミニポート\_SS\_特性**構造体。

選択的 NDIS のアイドル状態の通知を処理する方法の詳細については、中断を参照してください[NDIS セレクティブ サスペンド アイドル通知](ndis-selective-suspend-idle-notifications.md)します。

 

 





