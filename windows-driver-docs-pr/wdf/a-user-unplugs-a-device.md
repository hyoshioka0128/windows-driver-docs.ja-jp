---
title: ユーザーがデバイスを取り外す
description: ユーザーがデバイスを取り外す
ms.assetid: 85e69401-0128-4641-aa0f-fd7c4f22f395
keywords:
- PnP WDK KMDF、取り外しデバイス
- WDK KMDF のプラグアンドプレイ、デバイスの取り外し
- 正常にデバイスを削除する WDK KMDF
- デバイスの取り外し (WDK KMDF)
- 予期しないデバイス削除 WDK KMDF
- 予期しないデバイス削除 WDK KMDF
- WDK KMDF デバイスの削除
- デバイスの取り出し (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03da077748558cedb46da32145f2e56847aaf46
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242955"
---
# <a name="a-user-unplugs-a-device"></a>ユーザーがデバイスを取り外す


システムが実行されている間、ユーザーは2つの方法のいずれかでデバイスを削除できます。*つまり、デバイス*が削除されようとしていることをシステムに通知します (たとえば、プラグまたは取り出しハードウェアプログラムを使用して)。または、*突然削除*することによって、ユーザーがシステムに通知せずにデバイスを unplugs することになります。 バスで突然の削除 (USB など) がサポートされている場合、デバイスのドライバーはデバイスの突然の消失を処理できる必要があります。

### <a href="" id="orderly-removal"></a>正常に削除

ユーザーは、デバイスマネージャーを使用してデバイスを無効にするか、 [ejectable](supporting-ejectable-devices.md)デバイスの取り出しボタンを押すことによって、システムの取り外しまたは取り出しハードウェアプログラムを使用して削除を要求します。 このフレームワークでは、次のようなドライバーがない限り、デバイスを削除または無効にすることができます。

-   [**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)と呼ばれ、デバイス上で特別なファイルが開かれています。

-   [**Wdfdevicesetstaticstopremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)と呼ばれます。

-   指定された[*Evtdevicequeryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)コールバック関数が、コールバック関数によって削除が拒否されました。

デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの最上位にあるドライバーから、一度に1つのドライバーになります。

1.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数を呼び出します。

2.  このフレームワークは、すべてのドライバーの電源管理 i/o キューを停止します。

3.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)のコールバック関数 (存在する場合) を呼び出します。

4.  フレームワークは、ドライバーの[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled) callback 関数 (存在する場合) を呼び出し、各割り込みに対してドライバーの[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数 (存在する場合) を呼び出して、ドライバーがデバイスの割り込みを無効にできるようにします。

5.  フレームワークは、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数 (存在する場合) を呼び出します。

6.  このフレームワークは、ドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数 (存在する場合) を呼び出し、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースのリストを渡します。

7.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)コールバック関数を呼び出します。

8.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数を呼び出します。

バスドライバーは、最後に呼び出されるスタック内のドライバーです。 フレームワークがバスドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数を呼び出すと、コールバック関数はデバイス (バスの子デバイス) の電源状態を D3 に設定します。 バスドライバーは、フレームワークが[**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)を呼び出すことによって[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出すタイミングを制御できます。

### <a href="" id="surprise-removal"></a>突然の削除

ユーザーがデバイスを予期せず unplugs しています。 デバイスのバスのバスドライバーは、デバイスが不足していることを検出し、 [**WdfChildListUpdateChildDescriptionAsMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdatechilddescriptionasmissing)を呼び出します。

デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの最上位にあるドライバーから、一度に1つのドライバーになります。

1.  フレームワークは、ドライバーの[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバック関数 (存在する場合) を呼び出します。

2.  デバイスが切断されたときに動作 (D0) 状態になった場合、フレームワークはすべてのドライバーの電源管理 i/o キューを停止します。

3.  デバイスが切断されたときに動作 (D0) 状態にあった場合、およびドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)コールバック関数を呼び出します。

4.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)、および[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)のコールバック関数 (存在する場合) を呼び出します。

5.  このフレームワークは、ドライバーの[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数と[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数 (存在する場合) を呼び出して、ドライバーがデバイスの割り込みを無効にできるようにします。

6.  フレームワークは、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数 (存在する場合) を呼び出します。

7.  このフレームワークは、ドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数 (存在する場合) を呼び出し、PnP マネージャーがデバイスに割り当てたハードウェアリソースのリストを渡します。

8.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)コールバック関数を呼び出します。

9.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)コールバック関数を呼び出します。

デバイスは、いつでも予期せず削除される可能性があることに注意してください。 したがって、フレームワークは、前の手順で示したのとは別の方法で、ドライバーの[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal) callback 関数を呼び出す場合があります。 たとえば、ユーザーが[低電力状態に入っ](a-device-enters-a-low-power-state.md)ている間にデバイスを予期せず unplugs た場合、フレームワークは[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数を呼び出した後に[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal) callback 関数を呼び出す可能性があります。 [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバック関数は、それが特定のシーケンスで呼び出されることを前提としてコーディングしないでください。

さらに、このフレームワークは、デバイスの[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバック関数と、そのデバイスの前の手順で示されているコールバック関数を同期しません。 したがって、 [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal) callback 関数は、前述のコールバック関数が実行されている間に実行される可能性があります。

 

 





