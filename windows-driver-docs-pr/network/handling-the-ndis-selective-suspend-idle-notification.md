---
title: NDIS セレクティブ サスペンド アイドル通知の処理
description: NDIS セレクティブ サスペンド アイドル通知の処理
ms.assetid: 02D13260-5816-4621-8527-E1E79C9AE975
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7905c1fa5c2751be4d5bef961aac0c55fe2a1d00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579410"
---
# <a name="handling-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知の処理


選択的 NDIS 開始は、次のイベントのいずれかが発生した場合、操作を中断します。

-   ネットワーク アダプターは、アイドル状態のタイムアウト期間を超える active されました。 このタイムアウト期間がの値で指定された、  **\*SSIdleTimeout** INF キーワードを標準化します。 このキーワードの詳細については、次を参照してください。 [NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)します。

    NDIS がネットワーク アダプターがアイドル状態を決定する方法についての詳細については、次を参照してください。[方法 NDIS 検出アイドル状態のネットワーク アダプター](how-ndis-detects-idle-network-adapters.md)します。

-   常に 常に Connected (AOAC) テクノロジに準拠しているシステムは、コネクト スタンバイ状態に設定されています。

中断操作は、選択的で、ネットワーク アダプターが低電力状態に遷移しました。 NDIS は、呼び出すことによってこの操作を開始、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ミニポート ドライバーにアイドル状態の通知を発行するためのハンドラー関数。

ミニポート ドライバーは、アイドル状態の通知を処理する場合は、バスに依存するアクションを実行する必要があります。 次の図は、USB のネットワーク アダプターのミニポート ドライバーでアイドル状態の通知の処理に関連する手順を示します。

![アイドル状態の通知の操作を示す図](images/ndis-ss-idle-notification.png)

このトピックには、次が含まれています、NDIS 選択的に処理する方法については、アイドル状態の通知を中断します。

[呼び出しを処理するためのガイドライン*MiniportIdleNotification*](#guidelines-for-handling-the-call-to-miniportidlenotification)

[呼び出すのためのガイドライン**NdisMIdleNotificationConfirm**](#guidelines-for-the-call-to-ndismidlenotificationconfirm)

[アイドル状態の通知を中断をキャンセルして、選択的、NDIS の完了](#canceling-and-completing-an-ndis-selective-suspend-idle-notification)

## <a name="guidelines-for-handling-the-call-to-miniportidlenotification"></a>呼び出しを処理するためのガイドライン*MiniportIdleNotification*

NDIS ミニポート ドライバーおよび NDIS を呼び出すと次の手順をに従って[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092):

1.  NDIS 呼び出し、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)基になるネットワーク アダプターがアイドル状態であると思われるドライバーに通知ハンドラー関数。 NDIS セット、 *ForceIdle*のパラメーター、 *MiniportIdleNotification*次の値の 1 つのハンドラー関数。

    -   NDIS セット、 *ForceIdle*パラメーターを**FALSE**ときに、ネットワーク アダプターが非アイドルのタイムアウト期間よりも長くします。

    -   NDIS セット、 *ForceIdle*パラメーターを**TRUE**常に 常に Connected (AOAC) テクノロジに準拠しているシステムがコネクト スタンバイ状態に遷移するときにします。

2.  ときに[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)が呼び出され、ミニポート ドライバーがアイドル状態の通知を拒否し、選択的に NDIS を返すことによって操作を中断\_状態\_ビジーです。 たとえばのドライバーは、ドライバーには、ネットワーク アダプター上のアクティビティが検出された場合などに、アイドル状態の通知を拒否します。

    ミニポート ドライバーでは、アイドル状態の通知を vetoes、NDIS は、ネットワーク アダプター上のアクティビティの監視を再起動します。 NDIS を呼び出す場合は、アダプターは、アイドル状態のタイムアウト期間内でもう一度非アクティブになると、 [ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)します。

    **注**場合、ミニポート ドライバーはアイドル状態の通知を拒否しない必要があります、 *ForceIdle*にパラメーターが設定されている**TRUE**します。 この場合、ドライバーを続ける必要があります、選択的に操作を中断します。

3.  ミニポート ドライバーがアイドル状態の通知を拒否しては場合は、選択的な操作を中断するために、ネットワーク アダプターを準備する bus 固有操作を実行にする必要があります。 たとえば、USB のネットワーク アダプターのミニポート ドライバーは、ネットワーク アダプターが、低電力状態に移行できるかどうかを判断するには、次の手順を実行します。

    1.  ミニポート ドライバー呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) USB アイドル状態の要求の I/O 要求パケット (IRP) を発行する ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) を基になる USB バス ドライバー。 この IRP では、ミニポート ドライバーはコールバックと完了ルーチンを指定する必要があります。

        USB バス ドライバーが IRP を直ちに完了することはできません。 IRP が低電力の移行を保留中状態のままにします。 次のイベントのいずれかが発生すると、バス ドライバーを後で IRP が完了します。

        -   ミニポート ドライバーは IRP をキャンセルします。

        -   システム電源の状態の変更が必要です。

        -   デバイスは、USB ハブから削除されます。

    2.  USB バス ドライバーでは、低電力状態で、ネットワーク アダプターを配置できることを判断、ミニポート ドライバーの IRP のコールバック ルーチンを呼び出します。 この呼び出しは、ネットワーク アダプターが、低電力状態に移行することを確認します。

        USB のアイドル状態要求 IRP のコールバック ルーチンを作成する方法のガイドラインについては、次を参照してください。 [USB のアイドル状態要求 IRP のコールバック ルーチンを実装する](implementing-a-usb-idle-request-irp-callback-routine.md)します。

4.  ミニポート ドライバーには、選択的な中断操作のネットワーク アダプターの準備が完了すると、呼び出す[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)します。 この呼び出しでは、ミニポート ドライバーは、ネットワーク アダプターに移行する最下位の電源状態を指定します。

    バスの要件に応じて選択的操作、ミニポート ドライバーの呼び出しを中断[ **NdisMIdleNotificationConfirm** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)への呼び出しのコンテキストで同期的に[*MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)または後に非同期的に*MiniportIdleNotification*を返します。 たとえば、USB のミニポート ドライバーはネットワーク アダプターの呼び出し**NdisMIdleNotificationConfirm** USB アイドル状態の要求のコールバック ルーチンのコンテキスト内で。 USB バス ドライバー呼び出し、コールバック ルーチンへの呼び出しのコンテキストで同期的に[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または後に非同期的に*MiniportIdleNotification*返します。

5.  ミニポート ドライバーが NDIS を返す場合は、ネットワーク アダプターは、低電力状態に移行することができます、\_状態\_への呼び出しから PENDING [ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)します。

    **注**ミニポート ドライバー返します NDIS\_状態\_PENDING ドライバー呼び出されるまでアイドル状態の通知が完了していないため、 [ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491). ミニポート ドライバーが NDIS を返す必要がありますいない\_状態\_から成功[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)します。



ネットワーク アダプターが中断され、低電力状態に移行するまで、ミニポート ドライバーでは次の操作を実行する必要があります。

-   ミニポート ドライバーする必要があります受信パケットを処理し、呼び出すことで NDIS を示すため[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。

-   ミニポート ドライバーが完了した送信パケットを処理する必要があり、呼び出して NDIS を示すため[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)します。

    **注**NDIS ドライバーのコールしません[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)パケットを送信する関数[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)返します NDIS\_状態\_保留します。



## <a name="guidelines-for-the-call-to-ndismidlenotificationconfirm"></a>呼び出すのためのガイドライン**NdisMIdleNotificationConfirm**


NDIS およびミニポート ドライバー、ミニポート ドライバーを呼び出すと次の手順をに従って[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492):

1.  NDIS 問題[ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)基になるバス ドライバーにします。 この IRP では、外部のウェイク アップ シグナルへの応答内のネットワーク アダプターをウェイクするため、バス ドライバーを使用できます。

2.  オブジェクト識別子 (OID) を設定する NDIS 問題要求[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)ミニポート ドライバーにします。 この OID 要求が関連付けられている、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体をネットワーク アダプターにウェイク アップ イベントが生成されます。 設定を指定します。

    ミニポート ドライバーは、のメンバーの処理時にこれらのガイドラインに従う必要があります、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

    -   場合、 *ForceIdle*のパラメーター、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数の設定を FALSE に NDIS のみ設定、NDIS\_PM\_選択的\_SUSPEND\_有効フラグ、 **WakeUpFlags**のメンバー、 [ **NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。 ここでは、ネットワーク アダプターは、次のイベントのいずれかが発生したときに、ウェイク アップ イベントを通知できます。

        -   ネットワーク アダプターでは、受信パケットのフィルターに一致するパケットを受信します。 これらのフィルターのセット要求を OID を使用するアダプターが構成されている[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

        -   ネットワーク アダプターでは、メディアの切断または接続されているメディアのいずれかに、リンクの状態が変更されたときなど、ネットワーク ドライバー スタックによって処理が必要なその他の外部イベントを検出します。

    -   場合、 *ForceIdle*のパラメーター、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数に設定された**TRUE**NDIS は、NDIS を設定しません\_PM\_セレクティブ\_SUSPEND\_有効フラグ、 **WakeUpFlags**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。 この場合は、NDIS が他のメンバーを設定、 **NDIS\_PM\_パラメーター** NDIS 選択的に関連していないウェイク アップ イベントの中断の構造体します。

        **注**NDIS セット、 *ForceIdle*パラメーターを**TRUE**コネクト スタンバイ状態に常に 常に Connected (AOAC) テクノロジに準拠しているシステムが遷移中ときにのみです。

        ドライバーで NDIS OID 要求が完了すると\_状態\_成功します。

        **注**場合 NDIS 設定、NDIS\_PM\_セレクティブ\_中断\_有効フラグ、 **WakeUpFlags**のメンバー [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)の OID のセット要求を発行構造、 [OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)ミニポート ドライバーに直接します。 これにより、NDIS フィルター ドライバー、ネットワーク ドライバー スタック内で処理をバイパスします。

3.  OID の要求の設定後[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)が正常に完了したら、NDIS は OID セット要求を発行[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)ミニポート ドライバーにします。

    この OID セット要求を処理する場合、ドライバーは、OID 要求で指定されている低電力状態に遷移するネットワーク アダプターを準備します。 ドライバーは、次のように、すべての保留中の操作を完了する必要があります。

    -   以前に指定したすべてのミニポート ドライバー待機の呼び出しを通じて返されるパケットの受信[ *MiniportReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559437)します。

    -   ミニポート ドライバーでは、ハードウェアによって処理された送信要求を完了するまで待機します。 ミニポート ドライバーを呼び出す必要があります、要求が完了したら、 [ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)します。

    -   ミニポート ドライバーが呼び出すことですべての保留中の送信要求を完了[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)します。

    -   ミニポート ドライバーは保留中のすべての NDIS タイマーをキャンセルし、作業項目必要があります。 取り消された後、ドライバーはこれらのタイマーの完了を待つし、作業項目する必要があります。

    -   ミニポート ドライバーでは、休止状態のネットワーク アダプターを配置する必要があります。 たとえば、ドライバーは、すべてのハードウェア タイマーを取り消す必要があります。

    ミニポート ドライバーの OID のセットの要求で指定された以前指定したウェイク アップ イベントを有効にする基になるネットワーク アダプターを構成します[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)します。 ミニポート ドライバーの OID のセットの要求が完了すると、ネットワーク アダプターは、低電力の移行の準備ができたら、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780) NDIS に\_の状態\_成功しました。

4.  NDIS 問題、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)基になるバス ドライバーにします。 この IRP では、ネットワーク アダプターが、低電力状態に移行することを要求します。

    **注**中、選択的に中断操作は、ネットワーク アダプターへの呼び出しで指定されているデバイスの電源状態に移行されます[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)します。 ミニポート ドライバーでこのデバイスの電源状態を指定します、 *IdlePowerState*この関数のパラメーター。

NDIS がへの呼び出しから戻る IRP が完了すると、 [ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)します。

## <a name="canceling-and-completing-an-ndis-selective-suspend-idle-notification"></a>アイドル状態の通知を中断をキャンセルして、選択的、NDIS の完了

アイドル状態の通知が発行されると、取り消され、次の方法で完了することができます。

-   NDIS は、次の条件に該当する場合、未処理のアイドル状態の通知をキャンセルできます。

    -   上位のプロトコルまたはフィルター ドライバーをミニポート ドライバーに要求の送信パケットまたは OID の要求のいずれかを発行します。

    -   基になるアダプターでは、wake on LAN (WOL) のパターンに一致するパケットを受信またはメディア接続状態の変更を検出するなどのウェイク アップ イベントを通知します。

    NDIS は呼び出すことによって、アイドル状態の通知をキャンセル[ *MiniportCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464088)します。 このハンドラー関数が呼び出されると、ミニポート ドライバーは、アイドル状態の通知で以前発行がある可能性があります bus 固有 Irp をキャンセルします。 最後に、ミニポート ドライバーを呼び出す[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)アイドル状態の通知を完了します。

    NDIS がアイドル状態の通知をキャンセルする方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知をキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)します。

-   ネットワーク アダプターは、低電力状態が、ミニポート ドライバーでは電力状態にアダプターを再開する自体アイドル状態の通知を完了できます。 これを行う理由は、設計およびアダプターとドライバーの要件に固有です。 ミニポート ドライバーが呼び出すことにより、アイドル状態の通知を完了[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)します。

    ミニポート ドライバーがアイドル状態の通知を完了する方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知の完了](completing-the-ndis-selective-suspend-idle-notification.md)します。