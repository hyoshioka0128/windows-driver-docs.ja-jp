---
title: NDIS セレクティブ サスペンド ハンドラー関数の登録
description: NDIS セレクティブ サスペンド ハンドラー関数の登録
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a5ed25d93b7ed124fe9b3c31a0d404d27bb749
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842071"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>NDIS セレクティブ サスペンド ハンドラー関数の登録


ミニポートドライバーで NDIS 選択的中断がサポートされている場合、NDIS は、基になるネットワークアダプターがアイドル状態になったことをドライバーに通知します。 ミニポートドライバーは、これらのアイドル状態の通知を処理するために次の機能を提供する必要があります。

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)  
NDIS は、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出して、ネットワークアダプターがアイドル状態になったことをミニポートドライバーに通知します。 ミニポートドライバーは、ネットワークアダプターが低電力状態に移行できるかどうかを判断することによって、アイドル状態の通知を処理します。 ミニポートドライバーは、この決定をバス固有の方法で実行します。

たとえば、usb ミニポートドライバーは、USB アイドル要求に対して i/o 要求パケット (IRP) を発行して、ネットワークアダプターが低電力状態に移行できるかどうかを判断します ([**IOCTL\_内部\_usb\_送信\_アイドル状態\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を基になる USB バスドライバーに通知します。 この IRP を処理することで、アダプターがアイドル状態で、低電力状態に移行できることがミニポートドライバーに通知されます。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)  
NDIS は、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出して、未処理のアイドル状態の通知を取り消します。 この関数が呼び出されると、ミニポートドライバーは、アイドル状態の通知に対して以前に発行された可能性があるバス固有の Irp をキャンセルします。

たとえば、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)が呼び出されると、usb ミニポートは、以前に発行された usb アイドル要求 IRP をキャンセルする必要があります。 IRP がキャンセルされると、ミニポートドライバーは、アダプターがフルパワー状態に移行できるようになったことを通知します。

ミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数が呼び出されると、ドライバーは次の手順に従って、その NDIS 選択的中断ハンドラー関数を登録します。

1.  ミニポートドライバーでは、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造の**SetOptionsHandler**メンバーを、ドライバーの[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数のエントリポイントに設定する必要があります。 ドライバーは[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出して、NDIS **\_ミニポート\_ドライバー\_の特性**構造を ndis に登録します。

2.  NDIS は、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)への呼び出しのコンテキストで[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出します。

    [*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)が呼び出されると、ミニポートドライバーは、ハンドラー関数へのポインターを使用して、 [**NDIS\_ミニポート\_SS\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics)の構造体を初期化します。 次に、ミニポートドライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)を呼び出し、次*に、このパラメーターを*、 **NDIS\_ミニポート\_SS\_特性**の構造へのポインターに設定します。

NDIS の選択的中断に対するアイドル状態の通知を処理する方法の詳細については、「 [ndis の選択的中断のアイドル通知](ndis-selective-suspend-idle-notifications.md)」を参照してください。

 

 





