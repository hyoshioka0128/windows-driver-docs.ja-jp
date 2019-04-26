---
title: NDIS セレクティブ サスペンド アイドル通知のキャンセル
description: NDIS セレクティブ サスペンド アイドル通知のキャンセル
ms.assetid: 14C19F15-9D0E-4F37-942C-7F7AFE1EBA0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 887127920a4a04574994d82744b50570db3c1a4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351976"
---
# <a name="canceling-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知のキャンセル


ネットワーク アダプターは、アイドル状態のタイムアウトで非アクティブになると、NDIS 開始、選択的中断操作を使用します。 、この操作では、ネットワーク アダプターは低電力状態に遷移しました。 NDIS は、ミニポート ドライバーにアイドル状態の通知を発行してこの操作を開始します。 この操作の詳細については、次を参照してください。 [、NDIS セレクティブ サスペンド アイドル状態の通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)します。

NDIS 呼び出し、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)基になるネットワーク アダプターがアイドル状態であると思われるドライバーに通知ハンドラー関数。 アイドル状態の通知が発行されると、NDIS キャンセル保留中のアイドル状態通知 1 つの場合または複数の次の条件に該当します。

-   上位のプロトコルまたはフィルター ドライバーをミニポート ドライバーに送信パケット要求であるか、オブジェクト識別子 (OID) 要求を発行します。

    NDIS がこのシナリオでアイドル状態の通知をキャンセルする方法の詳細については、次を参照してください。[ドライバーの関連アクティビティのため、アイドル状態の通知をキャンセル](#canceling-the-idle-notification-because-of-overlying-driver-activity)します。

-   基になるアダプターでは、パケットの受信またはメディア接続状態の変更を検出するなどのウェイク アップ イベントを通知します。

    NDIS がこのシナリオでアイドル状態の通知をキャンセルする方法の詳細については、次を参照してください。[ウェイク アップの事象に起因アイドル状態の通知をキャンセル](#canceling-the-idle-notification-because-of-wake-up-events)します。

NDIS は呼び出すことによって、アイドル状態の通知をキャンセル、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)基になるミニポート ドライバーのハンドラー関数。 この関数が呼び出されたときに、ミニポート ドライバーは電力状態にアダプターを再開するアイドル状態の通知を完了する必要があります。 このプロセスのガイドラインについては、次を参照してください。 [NDIS 選択的な中断アイドル状態の通知の完了](completing-the-ndis-selective-suspend-idle-notification.md)します。

実装する方法について、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)ハンドラー関数を参照してください[実装、 *MiniportCancelIdleNotification*ハンドラー関数](implementing-a-miniportcancelidlenotification-handler-function.md)します。

## <a name="canceling-the-idle-notification-because-of-overlying-driver-activity"></a>ドライバのアクティビティを後続のため、アイドル状態の通知をキャンセル


NDIS モニターは、要求を送信し、OID 要求がネットワーク アダプターが中断されているし、低電力状態にある、ミニポート ドライバーに発行されます。 このような場合は、NDIS は、ネットワーク アダプターが電力状態に再開できるように、未処理のアイドル状態の通知をキャンセルします。

NDIS ミニポート ドライバーおよびアイドル状態の通知が取り消されたときにこれらの手順に従います。

1.  NDIS 呼び出し、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)未処理のアイドル状態の通知をキャンセル ハンドラー関数。 このハンドラー関数が呼び出されたときに、ミニポート ドライバーは、bus 固有 I/O 要求パケット (Irp)、アイドル状態の通知に対して以前発行がある可能性がありますを取り消す必要があります。

    たとえば、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)を呼び出すときは、ミニポート USB のネットワーク アダプターは、次の手順を実行します。

    1.  ミニポート ドライバーは保留中の USB アイドル状態の要求を取り消します ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) IRP します。 ミニポート ドライバーは、NDIS ドライバーが呼び出されたときにこの IRP を基になる USB バス ドライバー以前発行[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)関数。 ミニポート ドライバーが呼び出すことによってこの IRP を取り消します[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)します。

    2.  バス ドライバーが IRP USB アイドル状態要求をキャンセルすると、IRP のミニポート ドライバーの完了ルーチンを呼び出します。 この呼び出しでは、IRP が完了し、ネットワーク アダプターが電力状態に移行するドライバーに通知します。 ドライバーを呼び出し、完了ルーチンのコンテキストから[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491) NDIS ネットワーク アダプターを電力状態に移行できることを通知します。

    **注**ミニポート ドライバーを呼び出す bus 固有のアイドル状態の要求をキャンセルする依存関係に応じて[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)いずれかのコンテキストで同期的に、呼び出す[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)または後に非同期的に*MiniportCancelIdleNotification*を返します。

    USB アイドル要求 IRP の完了ルーチンを実装する方法の詳細については、次を参照してください。 [USB のアイドル状態要求 IRP の完了ルーチンを実装する](implementing-a-usb-idle-request-irp-completion-routine.md)します。

2.  ミニポート ドライバーでは、アイドル状態の通知、bus 固有 Irp をキャンセルした後に呼び出して[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)します。 この呼び出しでは、アイドル状態の通知が完了したこと、NDIS に通知します。 NDIS、オプションを選択し、完了するネットワーク アダプターを電力状態に遷移することによって操作を中断します。

    ときに[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)が呼び出されると、NDIS は、次の手順を実行します。

    1.  NDIS 問題[ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)基になるバス ドライバーにします。 この IRP では、ネットワーク アダプターの電源状態 PowerDeviceD0 を設定するバス ドライバーを要求します。

    2.  NDIS の OID セット要求を発行する[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)ミニポート ドライバーにします。 この OID 要求では、NDIS は、ネットワーク アダプターが NdisDeviceStateD0 の電力状態に遷移するようになりましたことを指定します。

        この OID セット要求を処理する場合、ドライバーは、電力の操作のアダプターを準備します。 これにより、復元、受信が含まれていて、エンジンを低電力状態に遷移する前と同じ状態に送信します。 ドライバー完了 NDIS に OID 要求\_状態\_成功します。

次の図は、NDIS USB のネットワーク アダプターのミニポート ドライバーに発行されたアイドル状態の通知をキャンセルしたときに関連する手順を示します。

![アイドル状態の通知の再開プロセスを示す図](images/ndis-ss-idle-notification-resume.png)

## <a name="canceling-the-idle-notification-because-of-wake-up-events"></a>ウェイク アップの事象に起因アイドル状態の通知をキャンセル


NDIS がの OID セット要求を発行するネットワーク アダプターは、低電力状態に移行する前に[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)ネットワーク アダプターにします。 この OID 要求では、アダプターに通知できます電力状態に再開するウェイク アップ イベントの種類を指定します。 選択的 NDIS 中断の次のウェイク アップ イベントのいずれかを通知するアダプターを構成します。

-   OID を構成したフィルターに一致するパケットの受信設定要求の[OID\_PM\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569764)または[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

-   アダプターのメディア接続の状態に変更されました。

NDIS ミニポート ドライバーおよび NDIS は、ネットワーク アダプターによって生成されたウェイク アップ シグナルによりアイドル状態の通知をキャンセルするとこれらの手順に従います。

1.  バス ドライバーが完了すると、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)は、アダプターは、低電力状態に遷移する前に NDIS によって発行されました。 IRP を完了するでは、バス ドライバーは、NDIS に対し、ネットワーク アダプタがウェイク アップのシグナルを生成したことを通知します。

2.  NDIS 呼び出し、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)ハンドラー関数をアイドル状態の通知をキャンセル操作を開始します。 この操作に関連する手順は、同じ」の説明に従って[ドライバーの関連アクティビティのため、アイドル状態の通知をキャンセル](#cancel-due-to-driver-activity)します。

たとえば、NDIS は、USB のネットワーク アダプターによって通知のウェイク アップ イベントのため、アイドル状態の通知をキャンセルしたときに関連する手順を次に示します。

![アイドル状態の通知のウェイク アップ プロセスを示す図](images/ndis-ss-idle-notification-resume-wake.png)









