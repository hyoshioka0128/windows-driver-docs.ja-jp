---
title: NDIS セレクティブ サスペンドの概要
description: NDIS セレクティブ サスペンドの概要
ms.assetid: D23E103E-893E-4B42-8EFD-0524846EF45F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 930e737e9911b1510002fe394a3d03882ce1adaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843737"
---
# <a name="overview-of-ndis-selective-suspend"></a>NDIS セレクティブ サスペンドの概要


Ndis 6.30 以降では、ndis の選択的中断インターフェイスを使用して、アダプターを低電力状態に移行することによって、NDIS でアイドル状態のネットワークアダプターを中断できます。 これにより、システムはアダプターの CPU と電力のオーバーヘッドを減らすことができます。

NDIS のセレクティブサスペンドは、USB v1.1 および v2.0 インターフェイスに基づくネットワークアダプターに特に便利です。 これらのアダプターは、アクティブであるかアイドル状態かに関係なく、受信したパケットに対して継続的にポーリングされます。 アイドル状態の USB アダプターを中断することで、CPU のオーバーヘッドを10% まで減らすことができます。

NDIS の選択的中断は、 [USB のセレクティブサスペンド](../usbcon/usb-selective-suspend.md)テクノロジに基づいています。 ただし、NDIS の選択的中断は、バスに依存しないように設計されています。 このようにして、選択的中断のバスに依存しない i/o 要求パケット (Irp) が NDIS によって発行されます。 これにより、ミニポートドライバーは、特定のバスのセレクティブサスペンドに必要な Irp を発行します。 たとえば、USB ネットワークアダプターのミニポートドライバーは、選択的中断中にバス固有の USB アイドル要求 IRP[ **\_(内部\_usb\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を usb バスドライバーに発行します。運用.

NDIS およびミニポートドライバーは、次の方法で NDIS の選択的中断に参加します。

1.  ミニポートドライバーによって NDIS の選択的中断のサポートが登録されている場合、NDIS はネットワークアダプターの i/o 動作を監視します。 I/o アクティビティには、受信パケットの表示、送信パケットの完了、およびミニポートドライバーによって処理される OID 要求が含まれます。

2.  NDIS では、指定されたアイドルタイムアウト期間を超えて非アクティブになっている場合、ネットワークアダプターがアイドル状態であると見なされます。 この場合、NDIS は、ネットワークアダプターを低電力状態に遷移させるために、ミニポートドライバーにアイドル通知を発行することで、セレクティブサスペンド操作を開始します。

    > [!NOTE]
    > アイドルタイムアウト時間の長さは、 **\*SSIdleTimeout**標準化された INF キーワードの値によって指定されます。 このキーワードの詳細については、「 [NDIS 選択的中断の標準化](standardized-inf-keywords-for-ndis-selective-suspend.md)された INF キーワード」を参照してください。     

    NDIS がネットワークアダプターがアイドル状態であると判断した場合の詳細については、「 [ndis がアイドル状態のネットワークアダプターを検出する方法](how-ndis-detects-idle-network-adapters.md)」を参照してください。

3.  NDIS は、ドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数を呼び出すことによって、ミニポートドライバーに対するアイドル通知を発行します。 この関数が呼び出されると、ミニポートドライバーは、ネットワークアダプターが低電力状態に移行できるかどうかを判断します。 ミニポートドライバーは、この決定をバス固有の方法で実行します。

    たとえば、usb ミニポートドライバーは、USB アイドル要求\_IRP を発行することによって、ネットワークアダプターが低電力状態に移行できるかどうかを判断します。これを行うには、[**内部\_usb\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を送信します。基になる USB バスドライバー。 これは、ネットワークアダプターがアイドル状態であることをバスドライバーに通知し、アダプターが低電力状態に移行できるかどうかを確認します。
    
    > [!NOTE]
    > ミニポートドライバーでは、USB アイドル要求 IRP のコールバックと完了ルーチンを指定する必要があります。
    
    ミニポートドライバーがアイドル状態の通知を処理する方法の詳細については、「 [NDIS の選択的中断を待機する通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

4.  ミニポートドライバーは、ネットワークアダプターが低電力状態に移行できることを確認した後、 [**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出します。 この呼び出しでは、ミニポートドライバーによって、ネットワークアダプターが遷移できる最も低い電源状態が指定されます。

5.  [**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)が呼び出されると、NDIS はミニポートドライバーに対して OID 要求を発行して、低電力状態に移行するためのアダプターを準備します。 また、NDIS は、アダプターを低電力状態に設定するために、基になるバスドライバーに Irp を発行します。

6.  ネットワークアダプターは、中断された後も、未処理のアイドル状態の通知が取り消されるまで、低電力状態のままになります。

    NDIS は、ミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)ハンドラー関数を呼び出すことによって、未処理のアイドル状態の通知をキャンセルします。 次の1つ以上の条件に該当する場合、NDIS はこのハンドラー関数を呼び出します。

    -   NDIS は、プロトコルまたはフィルタードライバーからミニポートドライバーに発行された送信パケット要求または OID 要求を検出します。

    -   ネットワークアダプターはウェイクアップイベントを通知します。 これは、アダプターがパケットを受信したとき、またはメディア接続状態の変化を検出したときに発生する可能性があります。

    ネットワークアダプターが中断された後、ミニポートドライバーは、アダプターをフルパワー状態に再開するために、アイドル状態の通知を完了することもできます。 これを行う理由は、ドライバーとアダプターの設計と要件に固有のものです。

    NDIS がアイドル状態の通知をキャンセルする方法の詳細については、「 [ndis の選択的中断のアイドル通知を取り消す](canceling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

    ミニポートドライバーがアイドル状態の通知を完了する方法の詳細については、「 [NDIS の選択的中断のアイドル通知を完了](completing-the-ndis-selective-suspend-idle-notification.md)する」を参照してください。

7.  [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) handler 関数が呼び出されると、ミニポートドライバーは、ネットワークアダプターをフルパワー状態に再開できるかどうかを判断します。 また、ドライバーは、アイドル状態の通知に対して以前に発行された可能性があるバス固有の Irp をキャンセルします。

    ネットワークアダプターがフルパワー状態に移行できるかを判断するには、バス固有のものを使用します。 たとえば、 [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)が呼び出されると、usb ミニポートは、以前に発行された usb アイドル要求 IRP をキャンセルする必要があります。 USB ドライバーが IRP をキャンセルするとすぐに、irp の完了ルーチンを呼び出して、IRP が取り消され、ネットワークアダプターがフルパワー状態に戻ることができることを確認します。 完了ルーチンのコンテキストでは、ミニポートドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出します。

    ネットワークアダプターがフルパワー状態に再開できることがミニポートによって判断されると、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されます。 この呼び出しは、アイドル状態の通知が完了したことを NDIS に通知します。 その後、NDIS は、ネットワークアダプターをフルパワー状態に移行することで、セレクティブサスペンド操作の完了に進みます。

8.  [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されると、NDIS はミニポートドライバーに OID 要求を発行して、フルパワー状態への移行を行うアダプターを準備します。 また、NDIS は、アダプターをフルパワー状態に設定するために、基になるバスドライバーに Irp を発行します。

9.  ネットワークアダプターがフルパワー状態になると、セレクティブサスペンド操作が完了します。 NDIS は、ネットワークアダプターの i/o アクティビティの監視を再開します。 別のアイドルタイムアウト時間が経過した後にアダプターが非アクティブになった場合、NDIS はネットワークアダプターを中断するためにミニポートドライバーに対してアイドル状態の通知を発行します。