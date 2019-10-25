---
title: PnP マネージャーがシステム リソースを再配布する
description: PnP マネージャーがシステム リソースを再配布する
ms.assetid: fc88ae0a-5b78-4292-a101-29d2fc383555
keywords:
- PnP WDK KMDF、リソースの再配布
- WDK KMDF のプラグアンドプレイ、リソースの再配布
- リソース再配布 (WDK KMDF)
- リソースの再配布 (WDK KMDF)
- パワーダウンシーケンス WDK KMDF
- パワーアップシーケンス WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf7720c2566e362bb151072809af8fc8711cf487
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831598"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP マネージャーがシステム リソースを再配布する


ユーザーがデバイスをシステムに追加し、PnP マネージャーが既に別のデバイスに割り当てているシステムリソースがデバイスに必要な場合は、PnP マネージャーがリソースの再割り当てを試行します。

このプロセスの間、PnP マネージャーはデバイスを停止し、動作 (D0) 状態から除外します。 その後、新しいリソースリストがデバイスに配信され、新しいリソースを使用して再起動できるようになります。

リソースを再配布するとき、デバイスのドライバーのいずれかに次のようなデバイスのリソースの割り当てが変更されることはありません。

-   [**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)と呼ばれ、デバイス上で特別なファイルが開かれています。

-   [**Wdfdevicesetstaticstopremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)と呼ばれます。

-   が[*Evtdevicequerystop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)コールバック関数を提供し、コールバック関数が再割り当てを拒否しました。

### <a name="power-down-sequence"></a>電源ダウンシーケンス

停止しているデバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの一番上にあるドライバーから、一度に1つずつ実行されます。

1.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数を呼び出します。

2.  フレームワークは、デバイスのすべての電源管理 i/o キューを停止します。

3.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)のコールバック関数を呼び出します。

4.  ドライバーの[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数と[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数 (存在する場合) を呼び出して、ドライバーがデバイスの割り込みを無効にできるようにします。

5.  フレームワークは、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数 (存在する場合) を呼び出します。

6.  このフレームワークは、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースのリストを渡すことによって、ドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数 (存在する場合) を呼び出します。

バスドライバーはスタック内の最下位のドライバーであり、最後に呼び出されます。 フレームワークは、バスドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数を呼び出すと、デバイスの PDO を表すフレームワークデバイスオブジェクトと**WdfPowerDeviceD3Final**の*targetstate*値を渡すハンドルを渡します。 バスドライバーは、フレームワークが[**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)を呼び出すことによって[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出すタイミングを制御できます。

### <a name="power-up-sequence"></a>電源投入シーケンス

最初に呼び出されるドライバーはバスドライバーです。 フレームワークがバスドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数を呼び出すと、コールバック関数はデバイス (バスの子デバイス) をその動作 (D0) 状態に復元します。

デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの一番下にあるドライバーから、一度に1つずつ実行されます。

1.  このフレームワークは、ドライバーの[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数 (存在する場合) を呼び出し、PnP マネージャーがデバイスに割り当てたハードウェアリソースの一覧を渡します。

2.  フレームワークは、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数 (存在する場合) を呼び出します。

3.  このフレームワークは、ドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)コールバック関数と[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数 (存在する場合) を呼び出して、ドライバーがデバイスの割り込みを有効にできるようにします。

4.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)、および[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)のコールバック関数を呼び出します。

5.  フレームワークは、ドライバーの[*Evtchildlistscanforchildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)コールバック関数 (存在する場合) を呼び出します。

6.  フレームワークは、デバイスのすべての電源管理 i/o キューを再起動します。

7.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)コールバック関数を呼び出します。

 

 





