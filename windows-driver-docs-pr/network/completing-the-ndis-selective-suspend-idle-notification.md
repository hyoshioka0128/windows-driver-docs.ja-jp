---
title: NDIS セレクティブ サスペンド アイドル通知の完了
description: NDIS セレクティブ サスペンド アイドル通知の完了
ms.assetid: 2330A8EE-DC8B-4244-935C-DEF20A6EB5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9132bcc874fca29dfe1440a81e1da3f6ef665160
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835157"
---
# <a name="completing-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知の完了


NDIS は、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出して、基になるネットワークアダプターがアイドル状態であると思われることをドライバーに通知します。 この操作の詳細については、「 [NDIS の選択的中断を待機する通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

アイドル状態の通知が発行されると、ミニポートドライバーは、次の条件下で NDIS のセレクティブサスペンドアイドル通知を完了します。

-   NDIS は、基になるミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出して、アイドル状態の通知をキャンセルします。

-   ミニポートドライバーは、アイドル状態の通知を完了します。 これを行う理由は、ドライバーとアダプターの設計と要件に固有のものです。 たとえば、ネットワークアダプターで受信アクティビティが検出された場合、ドライバーはアイドル状態の通知を完了できます。

ミニポートドライバーは、アイドル状態の通知を明示的に取り消すことができない  に**注意**してください。 NDIS がアイドル通知をキャンセルすると、このトピックで説明されているように、ミニポートドライバーが通知を完了する必要があります。 詳細については、「 [NDIS セレクティブサスペンドアイドル通知のキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

 

どちらの場合も、ミニポートドライバーはアイドル状態の通知を完了して、アダプターをフルパワー状態に再開する必要があります。 アイドル状態の通知を完了するには、ミニポートドライバーは、以前にアイドル通知に対して発行された可能性があるバス固有の i/o 要求パケット (Irp) をキャンセルする必要があります。 最後に、ドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出して、ネットワークアダプターをフルパワー状態に移行できることを NDIS に通知します。

たとえば、USB ネットワークアダプターのミニポートドライバーは、次の手順に従って、アイドル状態の通知を完了します。

1.  ミニポートドライバーは、保留中の USB アイドル要求 ([**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP をキャンセルします。 NDIS がドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)関数を呼び出したときに、ミニポートドライバーは、この IRP を基になる USB バスドライバーに以前に発行しました。 ミニポートドライバーは、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出すことによって、この IRP をキャンセルします。

2.  バスドライバーは、USB アイドル要求 IRP をキャンセルすると、その IRP のミニポートドライバーの完了ルーチンを呼び出します。 この呼び出しは、IRP が完了したこと、およびネットワークアダプターがフルパワー状態に移行できることをドライバーに通知します。 完了ルーチンのコンテキストからは、ドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出して、ネットワークアダプターをフルパワー状態に移行できることを NDIS に通知します。

    USB アイドル要求の IRP 完了ルーチンを実装する方法の詳細については、「 [Usb アイドル要求の Irp 完了ルーチンの実装](implementing-a-usb-idle-request-irp-completion-routine.md)」を参照してください。

**注**  は、バス固有のアイドル要求をキャンセルするための依存関係によっては、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)への呼び出しのコンテキストで同期的に、または*MiniportCancelIdleNotification*が返された後に非同期的に[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。

 

ミニポートドライバーは、アイドル状態の通知に対してバス固有の Irp をキャンセルした後、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。 この呼び出しは、アイドル状態の通知が完了したことを NDIS に通知します。 その後、NDIS はネットワークアダプターをフルパワー状態に移行することで、セレクティブサスペンド操作を完了します。

[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されると、NDIS は次の手順を実行します。

1.  NDIS では、IRP\_、基になるバスドライバーに[**電力\_設定\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されています。 この IRP は、バスドライバーに対して、ネットワークアダプターの電源状態を PowerDeviceD0 に設定するように要求します。

2.  NDIS では、オブジェクト識別子 (OID) set 要求の[oid\_PNP\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された\_電源をミニポートドライバーに設定します。 この OID 要求では、NDIS はネットワークアダプターが NdisDeviceStateD0 のフルパワー状態に移行するように指定しています。

    この OID セット要求を処理するときに、ドライバーはフルパワー操作のためにアダプターを準備します。 これには、受信エンジンと送信エンジンを、低電力状態に移行する前と同じ状態に復元することが含まれます。 次に、ドライバーは、NDIS\_STATUS\_SUCCESS の OID 要求を完了します。

次の図は、ミニポートドライバーが USB ネットワークアダプターに対してアイドル状態の通知を完了した場合に関係する手順を示しています。

![アイドル状態の通知再開プロセスを示す図](images/ndis-ss-idle-notification-complete.png)

**注**  ミニポートドライバーがアイドル状態の通知を完了した場合、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)への呼び出しによって以前に完了したアイドル状態の通知に対して[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出すことはできません。

 

 

 





