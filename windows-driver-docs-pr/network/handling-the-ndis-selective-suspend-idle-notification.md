---
title: NDIS セレクティブ サスペンド アイドル通知の処理
description: NDIS セレクティブ サスペンド アイドル通知の処理
ms.assetid: 02D13260-5816-4621-8527-E1E79C9AE975
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c674fde701b25421815e80978df49435ca425719
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842561"
---
# <a name="handling-the-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブ サスペンド アイドル通知の処理


次のいずれかのイベントが発生すると、NDIS はセレクティブサスペンド操作を開始します。

-   ネットワークアダプターがアイドルタイムアウト時間を超えて非アクティブになっています。 このタイムアウト期間の期間は、 **\*SSIdleTimeout**標準化された INF キーワードの値によって指定されます。 このキーワードの詳細については、「 [NDIS 選択的中断の標準化](standardized-inf-keywords-for-ndis-selective-suspend.md)された INF キーワード」を参照してください。

    NDIS がネットワークアダプターがアイドル状態であると判断した場合の詳細については、「 [ndis がアイドル状態のネットワークアダプターを検出する方法](how-ndis-detects-idle-network-adapters.md)」を参照してください。

-   Always On 常時接続 (通信) テクノロジに準拠しているシステムは、コネクトスタンバイ状態に移行されています。

セレクティブサスペンド操作を実行すると、ネットワークアダプターが低電力状態に移行します。 NDIS は、ミニポートドライバーへのアイドル通知を発行するために[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出すことによって、この操作を開始します。

ミニポートドライバーは、アイドル状態の通知を処理するときに、バスに依存するアクションを実行する必要がある場合があります。 次の図は、USB ネットワークアダプターのミニポートドライバーによるアイドル状態の通知の処理に関連する手順を示しています。

![アイドル状態の通知操作を示す図](images/ndis-ss-idle-notification.png)

このトピックでは、NDIS の選択的中断アイドル通知を処理する方法について、次の情報を示します。

[*MiniportIdleNotification*の呼び出しを処理するためのガイドライン](#guidelines-for-handling-the-call-to-miniportidlenotification)

[**NdisMIdleNotificationConfirm**の呼び出しに関するガイドライン](#guidelines-for-the-call-to-ndismidlenotificationconfirm)

[NDIS セレクティブサスペンドアイドル通知のキャンセルと完了](#canceling-and-completing-an-ndis-selective-suspend-idle-notification)

## <a name="guidelines-for-handling-the-call-to-miniportidlenotification"></a>*MiniportIdleNotification*の呼び出しを処理するためのガイドライン

Ndis とミニポートドライバーは、NDIS が[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)を呼び出すときに、次の手順に従います。

1.  NDIS は、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数を呼び出して、基になるネットワークアダプターがアイドル状態であると思われることをドライバーに通知します。 NDIS は、 *MiniportIdleNotification* handler 関数の*ForceIdle*パラメーターを、次のいずれかの値に設定します。

    -   ネットワークアダプターがアイドルタイムアウト時間を超えて非アクティブになっている場合、NDIS は*ForceIdle*パラメーターを**FALSE**に設定します。

    -   Always On 常時接続 (通信) テクノロジに準拠しているシステムがコネクトスタンバイ状態に移行している場合、NDIS は*ForceIdle*パラメーターを**TRUE**に設定します。

2.  [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)が呼び出されると、ミニポートドライバーは、NDIS\_STATUS\_BUSY を返すことによって、アイドル通知とセレクティブサスペンド操作を拒否することができます。 たとえば、ドライバーがネットワークアダプターでの利用状況を検出した場合、ドライバーはアイドル状態の通知を拒否する可能性があります。

    ミニポートドライバーがアイドル状態の通知を vetoes した場合、NDIS はネットワークアダプターでのアクティビティの監視を再開します。 アイドルタイムアウト期間内にアダプターが再び非アクティブになると、NDIS は[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)を呼び出します。

    **メモ** *ForceIdle*パラメーターが**TRUE**に設定されている場合、ミニポートドライバーは、アイドル状態の通知を拒否することはできません。 この場合、ドライバーはセレクティブサスペンド操作を続行する必要があります。

3.  ミニポートドライバーがアイドル状態の通知を拒否していない場合は、任意のバス固有の操作を実行して、ネットワークアダプターのセレクティブサスペンド操作を準備する必要があります。 たとえば、USB ネットワークアダプターのミニポートドライバーは、次の手順を実行して、ネットワークアダプターが低電力状態に移行できるかどうかを判断します。

    1.  ミニポートドライバーは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、usb アイドル要求に対して i/o 要求パケット (IRP) を発行します。これは、基になる usb バスドライバーに[ **\_アイドル\_通知を送信\_、内部\_usb\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)します。 この IRP では、ミニポートドライバーでコールバックと完了ルーチンを指定する必要があります。

        USB バスドライバーは、IRP をすぐには完了しません。 IRP は、低電力の移行によって保留中の状態のままになります。 次のいずれかのイベントが発生すると、バスドライバーは後で IRP を完了します。

        -   ミニポートドライバーは、IRP をキャンセルします。

        -   システムの電源状態の変更が必要です。

        -   デバイスが USB ハブから削除されます。

    2.  USB バスドライバーは、ネットワークアダプターを低電力状態にすることができると判断した後、ミニポートドライバーの IRP コールバックルーチンを呼び出します。 この呼び出しにより、ネットワークアダプターが低電力状態に移行できることが確認されます。

        USB アイドル要求 IRP のコールバックルーチンを記述する方法に関するガイドラインについては、「 [Usb アイドル要求の Irp コールバックルーチンの実装](implementing-a-usb-idle-request-irp-callback-routine.md)」を参照してください。

4.  ミニポートドライバーは、選択的中断操作のためにネットワークアダプターの準備を完了すると、 [**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出します。 この呼び出しでは、ミニポートドライバーによって、ネットワークアダプターが遷移できる最も低い電源状態が指定されます。

    セレクティブサスペンド操作のバス要件に応じて、ミニポートドライバーは[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)の呼び出しのコンテキストで同期的に呼び出すか、または非同期*的に呼び出します。MiniportIdleNotification*はを返します。 たとえば、USB ネットワークアダプターのミニポートドライバーは、USB アイドル要求のコールバックルーチンのコンテキスト内で**NdisMIdleNotificationConfirm**を呼び出します。 USB バスドライバーは、コールバックルーチンを[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)の呼び出しのコンテキストで同期的に呼び出すか、 *MiniportIdleNotification*がを返すと非同期的に呼び出します。

5.  ネットワークアダプターを低電力状態に移行できる場合、ミニポートドライバーは、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)への呼び出しからの NDIS\_STATUS\_PENDING を返します。

    **メモ** ミニポートドライバーは NDIS\_STATUS\_を返します。これは、ドライバーが[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出すまで、アイドル状態の通知が完了しないためです。 ミニポートドライバーは、 [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)から NDIS\_STATUS\_SUCCESS を返さないようにする必要があります。



ミニポートドライバーは、ネットワークアダプターが中断されて低電力状態に移行するまで、次の操作を実行する必要があります。

-   ミニポートドライバーは、受信したパケットを処理し、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによって NDIS に通知する必要があります。

-   ミニポートドライバーは、完了した送信パケットを処理し、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出すことによってそれらを NDIS に示す必要があります。

    **メモ** [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)が NDIS\_STATUS\_PENDING を返した場合、ndis はドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数を呼び出してパケットを送信しません。



## <a name="guidelines-for-the-call-to-ndismidlenotificationconfirm"></a>**NdisMIdleNotificationConfirm**の呼び出しに関するガイドライン


ミニポートドライバーが[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)を呼び出す場合、NDIS およびミニポートドライバーは次の手順に従います。

1.  NDIS は、基になるバスドライバーへの[**スリープ状態を解除\_\_待機**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)して、IRP の問題を\_します。 この IRP を使用すると、バスドライバーは外部のウェイクアップ信号に応答してネットワークアダプターをスリープ解除できます。

2.  NDIS は、オブジェクト識別子 (OID) set 要求の[oid\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)をミニポートドライバーに発行します。 この OID 要求は、ネットワークアダプターがウェイクアップイベントを生成する設定を指定する[**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体に関連付けられています。

    ミニポートドライバーは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体のメンバーを処理するときに、次のガイドラインに従う必要があります。

    -   [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数の*FORCEIDLE*パラメーターが FALSE に設定されている場合、ndis は、 [**WakeUpFlags のメンバーで、ndis\_PM\_選択的\_SUSPEND\_ENABLED フラグを設定します。NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体。 この場合、次のいずれかのイベントが発生すると、ネットワークアダプターはウェイクアップイベントを通知できます。

        -   ネットワークアダプターは、受信パケットフィルターに一致するパケットを受信します。 このアダプターは、Oid\_GEN の OID セット要求を使用して、[現在の\_パケット\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)フィルターを使用するように構成されています。

        -   ネットワークアダプターは、ネットワークドライバースタックによる処理を必要とする他の外部イベントを検出します。たとえば、リンクの状態がメディアの切断やメディアに接続されている場合などです。

    -   [*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数の*ForceIdle*パラメーターが**TRUE**に設定されている場合、ndis では、 **WakeUpFlags**メンバーで、NDIS\_PM\_選択的\_SUSPEND\_ENABLED フラグが設定されません。( [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体。 この場合、ndis は、ndis の選択的中断に関連しないウェイクアップイベントのために、 **ndis\_\_PM**の他のメンバーを設定します。

        **メモ** NDIS は、 *ForceIdle*パラメーターを**TRUE**に設定します。これは、Always On 常時接続 (通信) テクノロジに準拠しているシステムがコネクトスタンバイ状態に移行している場合に限ります。

        ドライバーは、NDIS\_STATUS\_SUCCESS の OID 要求を完了します。

        **メモ** Ndis\_PM\_選択的\_SUSPEND\_ENABLED フラグが ndis [ **\_pm\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**WakeUpFlags**メンバーに設定されている場合、このメソッドは OID\_pm の oid セット要求を発行[\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)をミニポートドライバーに直接渡す。 これにより、NDIS はネットワークドライバースタック内のドライバーをフィルター処理することによって処理をバイパスできます。

3.  Oid [\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)の oid セット要求が正常に完了した後、NDIS は、\_の電源をミニポートドライバーに設定する oid セット要求[OID\_\_PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)を発行します。

    この OID セット要求を処理するときに、ドライバーは、OID 要求に指定されている低電力状態に移行するようにネットワークアダプターを準備します。 ドライバーは、保留中のすべての操作を次の方法で完了する必要があります。

    -   ミニポートドライバーは、以前に示されたすべての受信パケットが[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)の呼び出しによって返されるのを待機します。

    -   ミニポートドライバーは、ハードウェアによって処理された送信要求が完了するまで待機します。 要求が完了すると、ミニポートドライバーは[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出す必要があります。

    -   ミニポートドライバーは、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出すことによって、すべての保留中の送信要求を完了します。

    -   ミニポートドライバーは、保留中のすべての NDIS タイマーと作業項目をキャンセルする必要があります。 これらの処理が取り消された後、ドライバーは、これらのタイマーと作業項目が完了するまで待機する必要があります。

    -   ミニポートドライバーは、ネットワークアダプターを休止状態にする必要があります。 たとえば、ドライバーはすべてのハードウェアタイマーをキャンセルする必要があります。

    ミニポートドライバーは、基になるネットワークアダプターを構成して、以前に oid set 要求で[oid\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)に指定されていたウェイクアップイベントを有効にします。 低電力の移行のためにネットワークアダプターを準備した後、ミニポートドライバーは oid\_PNP の OID セット要求を完了します。これにより、NDIS\_STATUS\_SUCCESS [\_電力が\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)されます。

4.  NDIS では、IRP\_、基になるバスドライバーに[**電力\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されています。 この IRP は、ネットワークアダプターが低電力状態に移行することを要求します。

    **メモ** セレクティブサスペンド操作中に、ネットワークアダプタは[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)の呼び出しで指定されたデバイスの電源状態に遷移します。 ミニポートドライバーは、この関数の*IdlePowerState*パラメーターでこのデバイスの電源状態を指定します。

IRP が完了すると、NDIS は[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)の呼び出しからを返します。

## <a name="canceling-and-completing-an-ndis-selective-suspend-idle-notification"></a>NDIS セレクティブサスペンドアイドル通知のキャンセルと完了

アイドル状態の通知が発行されると、次の方法でキャンセルおよび完了できます。

-   次の条件に該当する場合、NDIS は未処理のアイドル状態の通知を取り消すことができます。

    -   1つ上のプロトコルまたはフィルタードライバーが、ミニポートドライバーに送信パケット要求または OID 要求を発行します。

    -   基になるアダプターはウェイクアップイベントを通知します。たとえば、wake on LAN (WOL) パターンに一致するパケットを受信したり、メディア接続状態の変化を検出したりします。

    [*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)を呼び出すことによって、NDIS はアイドル状態の通知をキャンセルします。 このハンドラー関数が呼び出されると、ミニポートドライバーは、アイドル状態の通知に対して以前に発行された可能性があるバス固有の Irp をキャンセルします。 最後に、ミニポートドライバーは[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出して、アイドル状態の通知を完了します。

    NDIS がアイドル状態の通知をキャンセルする方法の詳細については、「 [ndis の選択的中断のアイドル通知を取り消す](canceling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

-   ネットワークアダプターが低電力状態になると、ミニポートドライバーはアイドル状態の通知を完了して、アダプターをフルパワー状態に戻すことができます。 これを行う理由は、ドライバーとアダプターの設計と要件に固有のものです。 ミニポートドライバーは、 [**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)を呼び出すことによって、アイドル状態の通知を完了します。

    ミニポートドライバーがアイドル状態の通知を完了する方法の詳細については、「 [NDIS の選択的中断のアイドル通知を完了](completing-the-ndis-selective-suspend-idle-notification.md)する」を参照してください。