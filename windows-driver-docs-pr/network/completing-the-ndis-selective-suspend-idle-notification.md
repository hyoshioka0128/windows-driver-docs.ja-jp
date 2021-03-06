---
title: NDIS セレクティブ サスペンド アイドル通知の完了
description: NDIS セレクティブ サスペンド アイドル通知の完了
ms.assetid: 2330A8EE-DC8B-4244-935C-DEF20A6EB5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fed191d205d963d4033a77415e5d85b99edf0ba8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379262"
---
# <a name="completing-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知の完了


NDIS 呼び出し、 [ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)基になるネットワーク アダプターがアイドル状態であると思われるドライバーに通知ハンドラー関数。 この操作の詳細については、次を参照してください。 [、NDIS セレクティブ サスペンド アイドル状態の通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)します。

ミニポート ドライバーが選択的 NDIS を完了すると、アイドル状態の通知が発行されると、次の条件下でアイドル状態の通知を中断します。

-   NDIS は呼び出すことによって、アイドル状態の通知をキャンセル、 [ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)基になるミニポート ドライバーのハンドラー関数。

-   ミニポート ドライバーでは、アイドル状態の通知自体を完了します。 これを行う理由は、設計およびアダプターとドライバーの要件に固有です。 たとえば、受信ネットワーク アダプターのアクティビティを検出した場合、ドライバーはアイドル状態の通知を完了でした。

**注**  ミニポート ドライバーからアイドル状態の通知を明示的にキャンセルすることはできません。 NDIS がアイドル状態の通知をキャンセルすると、ミニポート ドライバーはこのトピックの説明に従って通知を完了する必要があります。 詳細については、次を参照してください。 [NDIS 選択的な中断アイドル状態の通知をキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)します。

 

いずれの場合も、ミニポート ドライバーは、電力状態にアダプターを再開するアイドル状態の通知を完了する必要があります。 アイドル状態の通知を完了するには、ミニポート ドライバーは、bus 固有 I/O 要求パケット (Irp)、アイドル状態の通知に対して以前発行がある可能性がありますを取り消す必要があります。 最後に、ドライバーを呼び出す[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete) NDIS ネットワーク アダプターを電力状態に移行できることを通知します。

たとえば、USB のネットワーク アダプターのミニポート ドライバーでは、次の手順でアイドル状態の通知を実行します。

1.  ミニポート ドライバーは保留中の USB アイドル状態の要求を取り消します ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP します。 ミニポート ドライバーは、NDIS ドライバーが呼び出されたときにこの IRP を基になる USB バス ドライバー以前発行[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)関数。 ミニポート ドライバーが呼び出すことによってこの IRP を取り消します[ **IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)します。

2.  バス ドライバーが IRP USB アイドル状態要求をキャンセルすると、IRP のミニポート ドライバーの完了ルーチンを呼び出します。 この呼び出しでは、IRP が完了し、ネットワーク アダプターが電力状態に移行するドライバーに通知します。 ドライバーを呼び出し、完了ルーチンのコンテキストから[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete) NDIS ネットワーク アダプターを電力状態に移行できることを通知します。

    USB アイドル要求 IRP の完了ルーチンを実装する方法の詳細については、次を参照してください。 [USB のアイドル状態要求 IRP の完了ルーチンを実装する](implementing-a-usb-idle-request-irp-completion-routine.md)します。

**注**  ミニポート ドライバーを呼び出す bus 固有のアイドル状態の要求をキャンセルする依存関係に応じて[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)か同期的に呼び出しのコンテキストで[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)または後に非同期的に*MiniportCancelIdleNotification*を返します。

 

ミニポート ドライバーでは、アイドル状態の通知、bus 固有 Irp をキャンセルした後に呼び出して[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)します。 この呼び出しでは、アイドル状態の通知が完了したこと、NDIS に通知します。 NDIS、オプションを選択し、完了するネットワーク アダプターを電力状態に遷移することによって操作を中断します。

ときに[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されると、NDIS は、次の手順を実行します。

1.  NDIS 問題[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)基になるバス ドライバーにします。 この IRP では、ネットワーク アダプターの電源状態 PowerDeviceD0 を設定するバス ドライバーを要求します。

2.  オブジェクト識別子 (OID) を設定する NDIS 問題要求[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)ミニポート ドライバーにします。 この OID 要求では、NDIS は、ネットワーク アダプターが NdisDeviceStateD0 の電力状態に遷移するようになりましたことを指定します。

    この OID セット要求を処理する場合、ドライバーは、電力の操作のアダプターを準備します。 これにより、復元、受信が含まれていて、エンジンを低電力状態に遷移する前と同じ状態に送信します。 ドライバー完了 NDIS に OID 要求\_状態\_成功します。

次の図は、ミニポート ドライバーには、USB のネットワーク アダプターをアイドル状態の通知が完了すると関連する手順を示します。

![アイドル状態の通知の再開プロセスを示す図](images/ndis-ss-idle-notification-complete.png)

**注**  呼び出す必要がありますいないミニポート ドライバーでは、アイドル状態の通知が完了したら、 [ **NdisMIdleNotificationConfirm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)されていたアイドル状態の通知呼び出しを使用して完了[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)します。

 

 

 





