---
title: デバイスが低電力状態になる
description: デバイスが低電力状態になる
ms.assetid: 07d7c460-4316-40a9-b502-f7c1bd1182c2
keywords:
- 電源管理 WDK KMDF、低電力状態
- 低電力状態 WDK KMDF
- 電源状態が WDK KMDF
- デバイスの電源状態が WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- アイドル状態の電源切断 WDK KMDF
- 電源管理 WDK KMDF、アイドル状態の電源切断
- システム スリープ WDK KMDF を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe20ca1e3e1857130c72f1e7b6e6b4362f13aa8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385333"
---
# <a name="a-device-enters-a-low-power-state"></a>デバイスが低電力状態になる


デバイスは、その動作 (D0) 状態のままし、次のいずれかが発生した場合は低電力状態になります。

-   デバイスがアイドル状態 (にアクセスしていない) のシステムでの作業 (S0) 状態のまま、低電力アイドル状態を入力することができます。

-   システムの電源の状態は、低電力状態にその動作 (S0) 状態から変更されました。 (ドライバーを呼び出すことができます[ **WdfDeviceGetSystemPowerAction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)システムの電源の状態が変更された理由を特定します)。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最上位である driver 以降では、シーケンスで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数。

2.  フレームワークは、ドライバーの呼び出しや I/O キューの電源管理対象のすべてを停止、 [ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)コールバック関数 (存在する場合)。

3.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ *EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)、 [ *EvtDeviceArmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)、または[ *EvtDeviceArmWakeFromSxWithReason* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)コールバック関数。

4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [ *EvtDmaEnablerFlush* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[ *EvtDmaEnablerDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)作成 DMA チャネルごと (存在する) 場合にコールバックが機能します。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数 (存在する) 場合、し、呼び出し、ドライバーの[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数 (存在する) 場合、各割り込みのドライバーは、デバイスの割り込みを無効にできます。

6.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) (存在する) 場合、コールバック関数。

バス ドライバーは、最後に呼び出されるスタックのドライバーです。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)低電力状態にコールバック関数では、コールバック関数の設定 (バスの子デバイス) のデバイスの電源の状態。 フレームワークは、電源ポリシーの所有者が別の低電力状態を指定しない限り、D3 低電力状態を指定します。

 

 





