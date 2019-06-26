---
title: デバイスが動作状態に戻る
description: デバイスが動作状態に戻る
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- デバイスの電源状態が WDK KMDF
- 作業状態 WDK KMDF
- 電源状態が WDK KMDF
- システム ウェイク アップ WDK KMDF
- 電源管理 WDK KMDF、ウェイク アップ機能
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ecf5c3a87225e313f33e13d2bea1128cd9e765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385331"
---
# <a name="a-device-returns-to-its-working-state"></a>デバイスが動作状態に戻る


低電力状態にあるデバイスは、次のいずれかが発生した場合の稼働状態に返されます。

-   デバイスは、外部イベントを検出し、そのバス上ウェイク信号をトリガーします。 ウェイク信号の呼び出しを検出するバス ドライバー [ **WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)します。 結果として、フレームワークが、バス ドライバーの[ *EvtDeviceDisableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)コールバック関数。

-   デバイスがアイドル状態だったし、ドライバーは呼び出し[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)します。

-   システムの電源の状態は、低電力状態からの作業 (S0) 状態に変更されました。

フレームワークが、バス ドライバーをこのような状況の各に[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数は、作業 (D0) の状態 (バスの子デバイス) のデバイスを復元します。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (存在する) 場合、コールバック関数。

2.  フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)コールバック関数 (存在する) 場合の各中断し、呼び出し、ドライバーの[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数 (存在する) 場合、ドライバーには、デバイスの割り込みが有効にすることができます。

3.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [ *EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)と[ *EvtDmaEnablerSelfManagedIoStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)コールバックが作成された DMA チャネルごと (存在する) 場合に機能します。

4.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ *EvtDeviceDisarmWakeFromS0* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)または[ *EvtDeviceDisarmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)コールバック関数。

5.  フレームワークは、ドライバーの[ *EvtChildListScanForChildren* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) (存在する) 場合、コールバック関数。

6.  フレームワークの再起動のすべてのドライバーの電源管理対象の I/O キューと呼び出しの[ *EvtIoResume* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)コールバック関数 (必要な場合)。

7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)コールバック関数。

 

 





