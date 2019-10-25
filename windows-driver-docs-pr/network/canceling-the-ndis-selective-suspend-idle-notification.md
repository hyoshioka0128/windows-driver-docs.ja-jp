---
title: NDIS セレクティブ サスペンド アイドル通知のキャンセル
description: NDIS セレクティブ サスペンド アイドル通知のキャンセル
ms.assetid: 14C19F15-9D0E-4F37-942C-7F7AFE1EBA0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5ab12bdaecce1007cdb205b8eecebe3e0486407
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835247"
---
# <a name="canceling-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知のキャンセル


ネットワークアダプターがアイドルタイムアウト期間にわたって非アクティブになった場合、NDIS はセレクティブサスペンド操作を開始します。 この操作を実行すると、ネットワークアダプターが低電力状態に移行します。 NDIS は、ミニポートドライバーにアイドル通知を発行することによって、この操作を開始します。 この操作の詳細については、「 [NDIS の選択的中断を待機する通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

NDIS は、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出して、基になるネットワークアダプターがアイドル状態であると思われることをドライバーに通知します。 アイドル状態の通知が発行されると、次の1つ以上の条件に該当する場合、NDIS は保留中のアイドル状態の通知をキャンセルします。

-   1つ上のプロトコルまたはフィルタードライバーが、ミニポートドライバーに送信パケット要求またはオブジェクト識別子 (OID) 要求を発行します。

    このシナリオのために NDIS がアイドル状態の通知をキャンセルする方法の詳細については、「ドライバーのアクティビティが発生した[ため、アイドル状態の通知を取り消す](#canceling-the-idle-notification-because-of-overlying-driver-activity)」を参照してください。

-   基になるアダプターは、パケットの受信やメディア接続状態の変化の検出など、ウェイクアップイベントを通知します。

    このシナリオで NDIS がアイドル状態の通知をキャンセルする方法の詳細については、「[ウェイクアップイベントのためにアイドル状態の通知を取り消す](#canceling-the-idle-notification-because-of-wake-up-events)」を参照してください。

NDIS は、基になるミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出して、アイドル状態の通知をキャンセルします。 この関数が呼び出されると、ミニポートドライバーはアイドル状態の通知を完了して、アダプターを完全電源状態に再開する必要があります。 このプロセスのガイドラインについては、「 [NDIS の選択的中断のアイドル通知を完了する](completing-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を実装する方法の詳細については、「 [ *MiniportCancelIdleNotification* handler 関数の実装](implementing-a-miniportcancelidlenotification-handler-function.md)」を参照してください。

## <a name="canceling-the-idle-notification-because-of-overlying-driver-activity"></a>運転したドライバーの利用状況により、アイドル状態の通知を取り消しています


NDIS は、ネットワークアダプターが中断されており、低電力状態であるミニポートドライバーに発行された送信要求と OID 要求を監視します。 この場合、NDIS は未処理のアイドル状態の通知をキャンセルして、ネットワークアダプターがフルパワー状態に戻ることができるようにします。

NDIS およびミニポートドライバーは、アイドル状態の通知が取り消されたときに次の手順を実行します。

1.  NDIS は、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出して、未処理のアイドル状態の通知を取り消します。 このハンドラー関数が呼び出されると、ミニポートドライバーは、以前にアイドル通知に対して発行された可能性があるバス固有の i/o 要求パケット (Irp) をキャンセルする必要があります。

    たとえば、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)が呼び出されると、USB ネットワークアダプターのミニポートは次の手順を実行します。

    1.  ミニポートドライバーは、保留中の USB アイドル要求 ([**IOCTL\_内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP をキャンセルします。 NDIS がドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)関数を呼び出したときに、ミニポートドライバーは、この IRP を基になる USB バスドライバーに以前に発行しました。 ミニポートドライバーは、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出すことによって、この IRP をキャンセルします。

    2.  バスドライバーは、USB アイドル要求 IRP をキャンセルすると、その IRP のミニポートドライバーの完了ルーチンを呼び出します。 この呼び出しは、IRP が完了したこと、およびネットワークアダプターがフルパワー状態に移行できることをドライバーに通知します。 完了ルーチンのコンテキストからは、ドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出して、ネットワークアダプターをフルパワー状態に移行できることを NDIS に通知します。

    **メモ** バス固有のアイドル要求をキャンセルするための依存関係に応じて、ミニポートドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)の呼び出しのコンテキストで同期的に呼び出すか、または非同期的に呼び出します。*MiniportCancelIdleNotification*はを返します。

    USB アイドル要求の IRP 完了ルーチンを実装する方法の詳細については、「 [Usb アイドル要求の Irp 完了ルーチンの実装](implementing-a-usb-idle-request-irp-completion-routine.md)」を参照してください。

2.  ミニポートドライバーは、アイドル状態の通知に対してバス固有の Irp をキャンセルした後、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。 この呼び出しは、アイドル状態の通知が完了したことを NDIS に通知します。 その後、NDIS はネットワークアダプターをフルパワー状態に移行することで、セレクティブサスペンド操作を完了します。

    [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されると、NDIS は次の手順を実行します。

    1.  NDIS では、IRP\_、基になるバスドライバーに[**電力\_設定\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されています。 この IRP は、バスドライバーに対して、ネットワークアダプターの電源状態を PowerDeviceD0 に設定するように要求します。

    2.  NDIS は、\_電源をミニポートドライバーに設定する oid [\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) OID の oid セット要求を発行します。 この OID 要求では、NDIS はネットワークアダプターが NdisDeviceStateD0 のフルパワー状態に移行するように指定しています。

        この OID セット要求を処理するときに、ドライバーはフルパワー操作のためにアダプターを準備します。 これには、受信エンジンと送信エンジンを、低電力状態に移行する前と同じ状態に復元することが含まれます。 次に、ドライバーは、NDIS\_STATUS\_SUCCESS の OID 要求を完了します。

次の図は、NDIS が USB ネットワークアダプターのミニポートドライバーに発行されたアイドル通知をキャンセルした場合に関係する手順を示しています。

![アイドル状態の通知再開プロセスを示す図](images/ndis-ss-idle-notification-resume.png)

## <a name="canceling-the-idle-notification-because-of-wake-up-events"></a>ウェイクアップイベントのため、アイドル状態の通知を取り消しています


ネットワークアダプターが低電力状態に移行する前に、NDIS は oid [\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)の oid セット要求をネットワークアダプターに発行します。 この OID 要求では、アダプターがフルパワー状態に復帰するために通知できるウェイクアップイベントの種類を指定します。 NDIS のセレクティブサスペンドの場合、アダプタは次のいずれかのウェイクアップイベントを通知するように構成されています。

-   Oid\_PM の oid セット要求によって以前に構成されたフィルターに一致するパケットを受信しました。これは[\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)または[OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)を追加\_します.

-   アダプターのメディア接続状態の変更。

NDIS とミニポートドライバーは、ネットワークアダプターによって生成されたウェイクアップシグナルが原因で、NDIS がアイドル状態の通知をキャンセルするときに、次の手順に従います。

1.  バスドライバーは、アダプターを低電力状態に移行する前に、NDIS によって発行された[ **\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)によって IRP\_完了します。 IRP を完了すると、バスドライバーは、ネットワークアダプターがウェイクアップシグナルを生成したことを NDIS に通知します。

2.  NDIS は、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数を呼び出して、アイドル状態の通知をキャンセルする操作を開始します。 この操作に関連する手順は、「ドライバーの動作がこれ以上発生した[ため、アイドル状態の通知を取り消す](#canceling-the-idle-notification-because-of-overlying-driver-activity)」で説明した手順と同じです。

たとえば、次の図は、USB ネットワークアダプターによって通知されたウェイクアップイベントのために NDIS がアイドル状態の通知をキャンセルした場合に関係する手順を示しています。

![アイドル状態の通知ウェイクアッププロセスを示す図](images/ndis-ss-idle-notification-resume-wake.png)









