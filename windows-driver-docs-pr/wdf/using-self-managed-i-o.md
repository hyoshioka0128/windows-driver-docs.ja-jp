---
title: 自己管理型 I/O の使用
description: 自己管理型 I/O の使用
ms.assetid: 539b3618-44bb-41fd-a9f2-ed6a377c94e2
keywords:
- WDK KMDF、自己管理型の I/O を PnP します。
- プラグ アンド プレイ WDK KMDF、自己管理型の I/O
- 電源管理 WDK KMDF、自己管理型の I/O
- 自己管理型の I/O WDK KMDF
- I/O 自己管理 WDK KMDF
- デバイスの削除の WDK KMDF 驚くような
- 予期しないデバイスの削除の WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 618dd322624e95509e7be41cc23dc02dc6bd820e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372230"
---
# <a name="using-self-managed-io"></a>自己管理型 I/O の使用


ほとんどのフレームワークに基づいたドライバーでは、サポートされるデバイスのフレームワークの PnP や電源管理機能を活用します。 つまり、framework ベースのほとんどのドライバーでは、次の手順を実行して、デバイスの PnP、電源の状態を管理するために、フレームワークができます。

-   指定[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)と[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数。

-   指定[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)と[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数。

-   電源管理対象のキューの稼働状態にあるデバイスを必要とする I/O 要求を使用し、その他のすべての要求に対して電源管理されていないキューを使用します。

ただし、いくつかのフレームワークに基づいたドライバーには、次の状況でドライバーを含む、自分のデバイスの状態の大きい知識が必要です。

-   ドライバーを実行する操作は、ドライバーが framework I/O キューから受信した I/O 要求のセットによっては決定されません。

-   ドライバーは、古い framework 以外のドライバーと通信し、WDM インターフェイスを直接処理します。

-   ドライバーが受け取る I/O 要求は、2 つのグループに分割できない: 作業の状態とそうでないものにするデバイスを必要とします。

ほとんどのドライバーが前の状況では、いずれかでないが、ドライバーの場合は、デバイスの PnP、電源管理操作をより直接的に制御が必要があります。 このようなドライバーを使用できる*I/O を自己管理*します。 自己管理型の I/O を使用して、そのデバイスの電源接続時または、電源が入っていない場合、およびデバイスが一時的に停止されるたびに、(コールバック関数のセット) を使用して、ドライバーを通知することを意味します。

ドライバーできます自己管理型の I/O を使用し、依然として電源管理対象のキューのいずれかのフレームワークの I/O キューを使用するかに注意してください。 たとえば、ドライバーでは、一連の自己管理型の I/O のコールバック関数のいない電源の管理のフレームワークの I/O キューを使用できます。

呼び出すときに自己管理型の I/O を使用するドライバーは、余分なイベントのコールバック関数のセットに登録[ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)します。 これらのイベントのコールバック関数は次のとおりです。

-   [*EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)、初期化、およびデバイスの I/O 操作を開始します。

-   [*EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)、I/O 操作を中断します。

-   [*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)、中断された後は、デバイスの I/O 操作を再起動します。

-   [*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)、これは非対処の I/O 要求を削除します。

-   [*EvtDeviceSelfManagedIoCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)、によって割り当てられたリソースを解放する[ *EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)します。

デバイスでは、初めての作業 (D0) の状態が入ると、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数。 これは、毎回ユーザーに、システムにデバイスが接続されるため、システムを再起動するたびに発生します。

次の 3 つな状況で、ドライバーがデバイスの I/O 操作を停止する必要があります: デバイスが省電力状態に移行しようとしていますが削除される直前にまたはが予期せず削除されて既にします。 次の一覧には、このような状況の詳細の各が調べられます。

-   デバイスは、低電力状態にしは最終的に作業の状態を返します。

    デバイスが省電力状態の場合 (デバイスがアイドル状態になって、システム全体が、低電力状態を入力するかがあるため、PnP マネージャー[システムのハードウェア リソースを再配布](handling-requests-to-stop-a-device.md#redistributing-resources))、フレームワークによって、ドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数。 後の作業の状態をデバイスに入ります、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)コールバック関数。

-   デバイスは、削除しようとしています。

    処理するために[ユーザーが要求したデバイスの削除](handling-requests-to-stop-a-device.md#a-user-removes-or-disables-a-device)、フレームワークは、ドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)デバイスを停止する前に、コールバック関数。 デバイスを停止した後は、フレームワークは、ドライバーを呼び出します。 [ *EvtDeviceSelfManagedIoFlush* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)コールバック関数。 デバイスが削除された後、フレームワーク、 [ *EvtDeviceSelfManagedIoCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数。

-   デバイスが予期せず削除されて既に (突然の削除) します。

    デバイスのバスのドライバーは、デバイスが存在する場合は、不要になったことを決定します。 または、スタック内の別のドライバーは、デバイスが応答していないことを決定します。 場合は、問題が発見されたドライバーは PnP マネージャーに通知します。 PnP マネージャーはそのデバイスがなくなったことに、ドライバーの残りの部分を通知します。 フレームワーク ベースのドライバーでは、フレームワークは PnP マネージャーのメッセージを受信し、ドライバーの呼び出し[ *EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)、 [ *EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)、および[ *EvtDeviceSelfManagedIoCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数。

    (ドライバーにも登録できます、 [ *EvtDeviceSurpriseRemoval* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバック関数。 削除されたときの作業 (D0) 状態で、デバイスであった場合、フレームワーク*EvtDeviceSurpriseRemoval*自己管理型の I/O のコールバック関数を呼び出す前にします。 デバイスが削除されると、低電力状態だった場合*EvtDeviceSurpriseRemoval*が呼び出された後[ *EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend))

これで、フレームワーク ドライバーのイベントのコールバック関数、順序の詳細については、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

゚は必要ありません、ただし、フレームワークにより、ドライバーにアクセスして、デバイスの PnP、電源の状態をより詳細に制御を有効にして、[フレームワーク内のマシンの状態](state-machines-in-the-framework.md)します。

 

 





