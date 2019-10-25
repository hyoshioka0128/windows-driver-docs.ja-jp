---
title: デバイスが低電力状態になる
description: デバイスが低電力状態になる
ms.assetid: 07d7c460-4316-40a9-b502-f7c1bd1182c2
keywords:
- 電源管理 WDK KMDF、低電力状態
- 低電力状態 WDK KMDF
- 電源状態 WDK KMDF
- デバイスの電源状態 WDK KMDF
- スリープ電源管理 WDK KMDF
- アイドル状態の電源ダウン WDK KMDF
- 電源管理 WDK KMDF、アイドル電力ダウン
- システムのスリープ状態 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209556fd08bc474af22236a1dc3181fa11e657f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843657"
---
# <a name="a-device-enters-a-low-power-state"></a>デバイスが低電力状態になる


次のいずれかが発生すると、デバイスは動作中 (D0) 状態を維持し、低電力状態になります。

-   デバイスはアイドル状態 (つまり、アクセスされていません) であり、システムが動作中 (S0) 状態のままになっている間は、低電力アイドル状態に入ることができます。

-   システムの電源状態が動作中 (S0) から低電力状態に変わりました。 (ドライバーは[**WdfDeviceGetSystemPowerAction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)を呼び出して、システムの電源状態が変化している理由を判断できます)。

デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの最上位にあるドライバーから、一度に1つのドライバーになります。

1.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数を呼び出します。

2.  このフレームワークは、すべてのドライバーの電源管理 i/o キューを停止し、 [*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)コールバック関数を呼び出します (存在する場合)。

3.  ドライバーがデバイスの電源ポリシーの所有者である場合、フレームワークは[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)、 [*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)、または[*EvtDeviceArmWakeFromSxWithReason*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)のコールバック関数を呼び出します。

4.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)のコールバック関数 (存在する場合) を呼び出します。

5.  フレームワークは、ドライバーの[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled) callback 関数 (存在する場合) を呼び出し、割り込みごとにドライバーの[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) callback 関数 (存在する場合) を呼び出して、ドライバーが無効にできるようにします。デバイスの割り込み。

6.  フレームワークは、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数 (存在する場合) を呼び出します。

バスドライバーは、最後に呼び出されるスタック内のドライバーです。 フレームワークがバスドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数を呼び出すと、コールバック関数によって、デバイス (バスの子デバイス) の電源状態が低電力状態に設定されます。 このフレームワークは、電源ポリシーの所有者が異なる低電力状態を指定していない限り、D3 低電力状態を指定します。

 

 





