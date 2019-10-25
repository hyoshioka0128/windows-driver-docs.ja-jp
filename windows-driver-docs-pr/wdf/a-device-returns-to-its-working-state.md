---
title: デバイスが動作状態に戻る
description: デバイスが動作状態に戻る
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- デバイスの電源状態 WDK KMDF
- 作業状態 WDK KMDF
- 電源状態 WDK KMDF
- システムウェイクアップ WDK KMDF
- 電源管理 WDK KMDF、ウェイクアップ機能
- ウェイクアップ機能 WDK KMDF
- スリープ電源管理 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf921a1fb8c8d2c1857563979496467788497e4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843653"
---
# <a name="a-device-returns-to-its-working-state"></a>デバイスが動作状態に戻る


次のいずれかが発生した場合、低電力状態のデバイスは稼動状態に戻ります。

-   デバイスは外部イベントを検出し、そのバスで wake シグナルをトリガーします。 ウェイクアップ信号を検出するバスドライバー [**WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)を呼び出します。 その結果、フレームワークはバスドライバーの[*EvtDeviceDisableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)コールバック関数を呼び出します。

-   デバイスがアイドル状態で、ドライバーが[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出しました。

-   システムの電源状態が低電力状態から動作中 (S0) 状態に変わりました。

このような状況では、フレームワークはバスドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) callback 関数を呼び出します。これにより、デバイス (バスの子デバイス) が動作 (D0) 状態に復元されます。

デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの一番下にあるドライバーから、一度に1つずつ実行されます。

1.  フレームワークは、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数 (存在する場合) を呼び出します。

2.  フレームワークは、各割り込みのドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) callback 関数 (存在する場合) を呼び出し、ドライバーの[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled) callback 関数 (存在する場合) を呼び出して、ドライバーが有効にできるようにします。デバイスの割り込み。

3.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)、および[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)のコールバック関数 (存在する場合) を呼び出します。

4.  ドライバーがデバイスの電源ポリシーの所有者である場合、フレームワークはその[*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)または[*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx) callback 関数を呼び出します。

5.  フレームワークは、ドライバーの[*Evtchildlistscanforchildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)コールバック関数 (存在する場合) を呼び出します。

6.  フレームワークは、すべてのドライバーの電源管理 i/o キューを再起動し、必要に応じて、 [*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)コールバック関数を呼び出します。

7.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)コールバック関数を呼び出します。

 

 





