---
title: NDIS セレクティブ サスペンドの概要
description: NDIS セレクティブ サスペンドの概要
ms.assetid: D23E103E-893E-4B42-8EFD-0524846EF45F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba167fbc75c94f95acd8a69f467429af69f5e9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382654"
---
# <a name="overview-of-ndis-selective-suspend"></a>NDIS セレクティブ サスペンドの概要


NDIS 6.30 以降では、選択的の NDIS インターフェイスにより、アダプターを低電力状態に遷移することによって、アイドル状態のネットワーク アダプターを中断する NDIS を中断します。 これにより、CPU を削減し、アダプターのオーバーヘッドの電源をシステムができます。

選択的 NDIS 中断 USB v1.1 および v2.0 インターフェイスに基づくネットワーク アダプターに特に便利です。 これらのアダプターが受信したパケットはアクティブまたはアイドル状態かどうかに関係なく継続的にポーリングされます。 USB アダプターをアイドル状態を中断することによって、CPU のオーバーヘッドを 10% 削減できます。

選択的 NDIS 中断に基づいて、 [USB のセレクティブ サスペンド](../usbcon/usb-selective-suspend.md)テクノロジ。 ただし、中断して選択的 NDIS はバスに依存しない設計されています。 これで、バスに依存しないの I/O 要求パケット (Irp) の選択的な中断 NDIS によって発行されます。 これにより、ミニポート ドライバーに必要な任意の Irp の発行を担当選択時に特定のバスを中断します。 たとえば、ミニポート ドライバーの USB のネットワーク アダプター バスに固有の USB のアイドル状態の発行要求 IRP ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) USB バス ドライバー中に、選択的に操作を中断します。

NDIS およびミニポート ドライバーに参加次のように選択的 NDIS を中断します。

1.  ミニポート ドライバーには、選択的 NDIS のサポートが登録されている場合は、中断、NDIS は、ネットワーク アダプターの I/O アクティビティを監視します。 I/O のアクティビティを含む受信パケットの表示、パケットの入力候補、およびミニポート ドライバーによって処理される OID 要求を送信します。

2.  NDIS は、ネットワーク アダプターの場合、これが非アイドル タイムアウトを指定した期間よりも長くアイドル状態であると見なします。 このような場合は、選択的 NDIS 開始は、ネットワーク アダプターを低電力状態に移行するために、ミニポート ドライバーにアイドル状態の通知を発行して操作を中断します。

    > [!NOTE]
    > 値によって、アイドル状態のタイムアウト時間の長さが指定されて、  **\*SSIdleTimeout** INF キーワードを標準化します。 このキーワードの詳細については、次を参照してください。 [NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)します。     

    NDIS がネットワーク アダプターがアイドル状態を決定する方法についての詳細については、次を参照してください。[方法 NDIS 検出アイドル状態のネットワーク アダプター](how-ndis-detects-idle-network-adapters.md)します。

3.  NDIS ミニポート ドライバーを呼び出してドライバーのアイドル状態の通知を発行する[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数。 この関数が呼び出されたときに、ミニポート ドライバーは、ネットワーク アダプターが、低電力状態に移行できるかどうかを決定します。 ミニポート ドライバーでは、バスに固有の方法でこの決定を実行します。

    たとえば、USB ミニポート ドライバーは IRP USB アイドル状態要求を実行して、ネットワーク アダプターが低電力状態に移行できるかどうかを決定 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を基になる USB バス ドライバー。 バス ドライバーは、ネットワーク アダプターがアイドル状態し、アダプターを低電力状態に移行することができるかどうかを確認します。 この通知します。
    
    > [!NOTE]
    > ミニポート ドライバーでは、USB アイドル要求 IRP のコールバックと完了ルーチンを指定する必要があります。
    
    ミニポート ドライバーがアイドル状態の通知を処理する方法の詳細については、次を参照してください。 [、NDIS セレクティブ サスペンド アイドル状態通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)します。

4.  呼び出し後、ミニポート ドライバーでは、ネットワーク アダプターが、低電力状態に移行することを確認、 [ **NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)します。 この呼び出しでは、ミニポート ドライバーは、ネットワーク アダプターに移行する最下位の電源状態を指定します。

5.  ときに[ **NdisMIdleNotificationConfirm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)が呼び出されると、NDIS OID 要求を発行、ミニポート ドライバーでアダプターを備える低電力状態に遷移します。 NDIS は、アダプターを低電力状態に設定する基になるバス ドライバーにも Irp を発行します。

6.  ネットワーク アダプターが中断された後に未処理のアイドル状態の通知が取り消されるまで低電力状態には残ります。

    NDIS ミニポート ドライバーを呼び出すことによって、未処理のアイドル状態の通知をキャンセルする[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)ハンドラー関数。 NDIS は、1 つの場合は、このハンドラー関数を呼び出すまたは、次の条件の該当します。

    -   NDIS がパケットの送信要求を検出または OID 要求プロトコルまたはフィルター ドライバーを後続のミニポート ドライバーに発行されます。

    -   ネットワーク アダプターでは、ウェイク アップのイベントを通知します。 アダプターは、パケットを受信したり、メディア接続状態の変更が検出される場合があります。

    ネットワーク アダプターが中断された後、ミニポート ドライバーを使用電力状態にアダプターを再開するには、アイドル状態の通知を完了できます。 これを行う理由は、設計およびアダプターとドライバーの要件に固有です。

    NDIS がアイドル状態の通知をキャンセルする方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知をキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)します。

    ミニポート ドライバーがアイドル状態の通知を完了する方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知の完了](completing-the-ndis-selective-suspend-idle-notification.md)します。

7.  ときに、 [ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)ハンドラー関数が呼び出されると、ミニポート ドライバーが電力状態に、ネットワーク アダプターが再開できるかどうかを決定します。 ドライバーでは、アイドル状態の通知で以前発行がある可能性があります bus 固有 Irp もキャンセルします。

    ネットワーク アダプターが電力状態に移行する決定は、bus 固有です。 たとえば、 [ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)を呼び出すと、USB ミニポートが以前に発行された USB アイドル要求 IRP を取り消す必要があります。 USB ドライバーが IRP をキャンセルするとすぐに IRP が取り消され、電力状態に、ネットワーク アダプターが再開できることを確認 IRP の完了ルーチンを呼び出します。 ミニポート ドライバーが呼び出し完了ルーチンのコンテキストで[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)します。

    呼び出すミニポート判断されると、ネットワーク アダプターが電力状態に再開できます[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)します。 この呼び出しでは、アイドル状態の通知が完了したこと、NDIS に通知します。 NDIS し、選択的に完了できない処理の進行状況は、ネットワーク アダプターを電力状態に遷移することによって操作を中断します。

8.  ときに[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)が呼び出されると、NDIS OID 要求を発行、ミニポート ドライバーでアダプターを備える電力状態に遷移します。 NDIS は、アダプターを電力状態に設定する基になるバス ドライバーにも Irp を発行します。

9.  セレクティブ サスペンド操作電力状態に、ネットワーク アダプターの再開時が完了します。 NDIS は、ネットワーク アダプターの I/O 利用状況の監視を再開します。 アダプターは、別のアイドル状態のタイムアウト期間後に非アクティブになると、NDIS は、ネットワーク アダプターを中断するために、ミニポート ドライバーにアイドル状態の通知を発行します。