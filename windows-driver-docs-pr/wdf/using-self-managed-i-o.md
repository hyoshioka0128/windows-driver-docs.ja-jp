---
title: 自己管理型 I/O の使用
description: 自己管理型 I/O の使用
ms.assetid: 539b3618-44bb-41fd-a9f2-ed6a377c94e2
keywords:
- PnP WDK KMDF、自己管理型 i/o
- WDK KMDF、自己管理型 i/o のプラグアンドプレイ
- 電源管理 WDK KMDF、自己管理型 i/o
- 自己管理型 i/o WDK KMDF
- I/o セルフ管理 WDK KMDF
- 予期しないデバイス削除 WDK KMDF
- 予期しないデバイス削除 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d291fcabb8813d33e090d4a8b16d9f452e65884a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845431"
---
# <a name="using-self-managed-io"></a>自己管理型 I/O の使用


ほとんどのフレームワークベースのドライバーは、サポートするデバイスのために、フレームワークの PnP および電源管理機能を利用します。 つまり、ほとんどのフレームワークベースのドライバーでは、次のすべてを実行して、デバイスの PnP と電源の状態を管理できます。

-   [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)と[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)のコールバック関数を提供します。

-   [*EvtdeviceEvtDeviceReleaseHardware hardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)関数と[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を提供します。

-   I/o 要求に対して、電源管理キューを使用して、デバイスを動作状態にする必要があります。また、他のすべての要求に対して、電源管理されていないキューを使用します。

ただし、いくつかのフレームワークベースのドライバーでは、次のような状況でのドライバーを含む、デバイスの状態に関するより多くの知識が必要になります。

-   ドライバーが実行する操作は、ドライバーがフレームワークの i/o キューから受信する i/o 要求のセットによって決定されることはありません。

-   ドライバーは、従来の非フレームワークドライバーと通信し、WDM インターフェイスを直接処理します。

-   ドライバーが受信する i/o 要求は2つのグループに分けることができません。つまり、デバイスを動作状態にする必要があるものと、そうでないものがあります。

ほとんどのドライバーは、上記の状況の1つではありませんが、ドライバーがの場合は、デバイスの PnP および電源管理操作をより直接的に制御する必要があります。 このようなドライバーでは *、自己管理型の*i/o を使用できます。 自己管理型 i/o を使用するということは、デバイスが電源に接続されているか、接続が切断された場合、およびデバイスが一時的に停止された場合に、ドライバーが (コールバック関数のセットによって) 通知されることを意味します。

ドライバーは自己管理型 i/o を使用できますが、その場合でも、フレームワークの i/o キューは、電源管理キューとしても使用できます。 たとえば、ドライバーは、自己管理型の i/o コールバック関数のセットと共に、電源管理ではなく、フレームワークの i/o キューを使用できます。

自己管理型の i/o を使用するために、ドライバーは[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)を呼び出すときに、イベントコールバック関数の追加セットを登録します。 これらのイベントコールバック関数は次のとおりです。

-   [*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)。デバイスの i/o 操作を初期化して開始します。

-   [*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)。 i/o 操作を中断します。

-   [*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)。中断されたデバイスの i/o 操作を再開します。

-   [*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)。サービスされていない i/o 要求を削除します。

-   [*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)。 [*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)によって割り当てられたリソースを解放します。

デバイスが最初に動作中 (D0) 状態になると、フレームワークは、ドライバーの[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数を呼び出します。 これは、ユーザーがデバイスをシステムに接続するたび、およびシステムが再起動されるたびに発生します。

デバイスの i/o 操作をドライバーが停止する必要がある状況は3つあります。デバイスが低電力状態になるか、削除されようとしているか、予期せずに削除されています。 次の一覧では、これらの状況について詳しく説明します。

-   デバイスが低電力状態になり、最終的には動作状態に戻ります。

    デバイスが低電力状態に入ろうとしているとき (デバイスがアイドル状態になっているか、システム全体が低電力状態に入っているか、PnP マネージャーが[システムハードウェアリソース](handling-requests-to-stop-a-device.md#redistributing-resources)を再配布しているため)、フレームワークはドライバー[*を呼び出します。EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数。 デバイスが動作状態になった後、フレームワークはドライバーの[*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart) callback 関数を呼び出します。

-   デバイスを削除しようとしています。

    [ユーザーが要求したデバイスの削除](handling-requests-to-stop-a-device.md#a-user-removes-or-disables-a-device)を処理するために、フレームワークはデバイスを停止する前に、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数を呼び出します。 デバイスを停止した後、フレームワークはドライバーの[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush) callback 関数を呼び出します。 デバイスが削除されると、フレームワークは[*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数を呼び出します。

-   デバイスは予期せず削除されました (突然削除)。

    デバイスのバスのドライバーによってデバイスが存在しないと判断された場合、またはスタック内の別のドライバーによってデバイスが応答していないと判断された場合、問題を検出したドライバーは PnP マネージャーに通知します。 PnP マネージャーは、デバイスが失われたことを他のドライバーに通知します。 フレームワークベースのドライバーの場合、フレームワークは PnP マネージャーのメッセージを受信し、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)、 [*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)、および[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数を呼び出します。

    (ドライバーでは、 [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバック関数を登録することもできます。 デバイスが削除されたときに動作 (D0) 状態になった場合、フレームワークは、自己管理型の i/o コールバック関数を呼び出す前に*EvtDeviceSurpriseRemoval*を呼び出します。 デバイスが削除されたときに低電力状態になった場合、 *EvtDeviceSurpriseRemoval*は[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)の後に呼び出されます。

フレームワークがドライバーのイベントコールバック関数を呼び出す順序の詳細については、「 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)」を参照してください。

ほとんど必要ありませんが、フレームワークでは、[フレームワークのステートマシン](state-machines-in-the-framework.md)にアクセスすることによって、デバイスの PnP と電源の状態をさらに制御することができます。

 

 





