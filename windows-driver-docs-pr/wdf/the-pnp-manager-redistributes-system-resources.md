---
title: PnP マネージャーがシステム リソースを再配布する
description: PnP マネージャーがシステム リソースを再配布する
ms.assetid: fc88ae0a-5b78-4292-a101-29d2fc383555
keywords:
- PnP WDK KMDF、リソースの再配布
- プラグ アンド プレイ WDK KMDF、リソースの再配布
- リソースの再配布 WDK KMDF
- WDK KMDF のリソースを再配布
- 電源シーケンス WDK KMDF
- 電源投入シーケンス WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e939bed91c4fda56dffa861b20a192bfc11d6ce6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372304"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP マネージャーがシステム リソースを再配布する


ユーザーがシステムでは、デバイスを追加し、PnP マネージャーが別のデバイスに既に割り当てられているシステム リソースがデバイスに必要な場合、PnP マネージャーは、リソースを再割り当てを試みます。

このプロセス中には、PnP マネージャーは、デバイスを停止し、外の作業 (D0) 状態に移動します。 提供新しいリソースの一覧をデバイスに新しいリソースを使用して、再起動ができるようにします。

リソースを再頒布時に PnP マネージャーは変更されません、デバイスのリソースの割り当てがある、デバイスのドライバーのいずれかの場合。

-   呼ばれる[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)特別なファイルは、デバイスで開いているとします。

-   呼ばれる[ **WdfDeviceSetStaticStopRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)します。

-   指定された、 [ *EvtDeviceQueryStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)コールバック関数、およびコールバック関数を再割り当てが拒否しました。

### <a name="power-down-sequence"></a>シーケンスを電源

各関数とフィルター ドライバーを停止中でデバイスをサポートするために、フレームワークはシーケンス、ドライバー スタックの最上位である driver 以降では、一度に 1 つのドライバーで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数。

2.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを停止します。

3.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [ *EvtDmaEnablerFlush* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[ *EvtDmaEnablerDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)作成された DMA チャネルごとのコールバック関数。

4.  ドライバーの呼び出す[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)と[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数 (存在する場合)ドライバーは、デバイスの割り込みを無効にできます。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) (存在する) 場合、コールバック関数。

6.  フレームワークは、ドライバーの[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

バス ドライバー スタックの最下位のドライバーは、最後に呼び出されます。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数では、デバイスの PDO を表す framework デバイス オブジェクトをハンドルを渡しますが、 *TargetState* @property **WdfPowerDeviceD3Final**します。 フレームワークを呼び出すときに、バス ドライバーを制御できますその[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出して[  **。WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)します。

### <a name="power-up-sequence"></a>電源投入シーケンス

呼ばれる最初のドライバーは、バス ドライバーです。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数では、コールバック関数では、デバイス (バスの子デバイス) を作業 (D0) 状態に復元します。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

2.  フレームワークは、ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (存在する) 場合、コールバック関数。

3.  フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)と[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数 (存在する場合)、ドライバーがデバイスの割り込みを有効にするようにします。

4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [ *EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)と[ *EvtDmaEnablerSelfManagedIoStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)作成された DMA チャネルごとのコールバック関数。

5.  フレームワークは、ドライバーの[ *EvtChildListScanForChildren* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) (存在する) 場合、コールバック関数。

6.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを再起動します。

7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)コールバック関数。

 

 





