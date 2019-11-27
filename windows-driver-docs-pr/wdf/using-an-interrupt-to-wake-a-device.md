---
title: デバイスのウェイクに対する割り込みの使用
description: デバイスが低電力状態に移行すると、フレームワークは i/o 処理に使用される割り込み (または非アクティブとしてレポート) を切断します。
ms.assetid: 6A4E62BD-B10F-4F01-B4B4-1FF5086710D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270c36b954941d9cd518cc2d0f9cb636001fab69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843099"
---
# <a name="using-an-interrupt-to-wake-a-device"></a>デバイスのウェイクに対する割り込みの使用


デバイスが低電力状態に移行すると、フレームワークは i/o 処理に使用される割り込み (または非アクティブとしてレポート) を切断します。 Windows 8.1 で実行されている KMDF 1.13 と UMDF 2.0 以降では、WDF ドライバーは、デバイスが低電力状態に遷移したときにアクティブなままになるフレームワークの割り込みオブジェクトを作成できます。その後、デバイスを停止して、完全な D0 状態に復元するために使用できます。

チップ (SoC) プラットフォーム上のシステム用の WDF ドライバーを開発している場合は、このような割り込みを使用して、従来の wake シグナリングメカニズムを備えていないデバイスをウェイクアップできます。 この機能を使用するには、デバイスが、ACPI を介して公開される wake 割り込みに対するハードウェアサポートを備えている必要があります。 割り込みを作成するドライバーは、デバイスの電源ポリシーの所有者である必要があります。

デバイスが低電力状態に移行しても、ウェイクアップ対応として識別された割り込みが切断されることはありません。 デバイスが割り込みを行うと、このフレームワークは、IRQL = パッシブ\_レベルでドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)および[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバックルーチンを呼び出します。

ドライバーで i/o 処理用の[パッシブレベルの割り込みオブジェクト](supporting-passive-level-interrupts.md)が既に作成されている場合は、その同じ割り込みオブジェクトを wake 機能用に共有することをお勧めします。 このシナリオでは、ドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバックルーチンによって、i/o 関連の割り込みおよびスリープ処理の処理を実行するための条件付きロジックが実装されます。

ただし、ドライバーがデバイスの IRQL (DIRQL) での処理を必要とする割り込みを使用する場合は、ウェイクアップ機能を提供するために、追加のフレームワーク割り込みオブジェクトを作成することをお勧めします。

KMDF または UMDF ドライバーで wake 対応の割り込みオブジェクトを作成するには、次の手順に従います。

1.  [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出します。通常は、 *IdleCaps*パラメーターで**IdleCanWakeFromS0**を指定して、 [*evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)から呼び出します。
2.  必要に応じて、 [**Wdfdeviceinitsetpowerpolicyeventcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)を呼び出して、「[システムウェイクアップのサポート](supporting-system-wake-up.md)」で説明されているイベントコールバック関数を登録します。
3.  [**WDF\_interrupt\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdf_interrupt_config_init)を呼び出して、 [**WDF\_interrupt\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体を初期化します。 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数を指定します。このコールバック関数は、パッシブレベルで呼び出されます。 構成構造で、「CanWakeDevice **Veハンドリング**」と 「 **TRUE**」に設定します。 次に[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 、ドライバーの[*EvtdeviceWdfInterruptCreate ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数から、フレームワークの interrupt オブジェクトを作成するためのコールバック関数を呼び出します。
4.  [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)を呼び出して、システムを低電力状態からウェイクアップするようにデバイスを構成します。
    ```cpp
    WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
    wakeSettings.DxState = PowerDeviceD3;
    wakeSettings.UserControlOfWakeSettings = WakeDoNotAllowUserControl;
    wakeSettings.Enabled = WdfTrue;

    status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
    if (!NT_SUCCESS(status)) {
        Trace(TRACE_LEVEL_ERROR,"WdfDeviceAssignSxWakeSettings failed %x\n", status);
        return status;
    }
    ```

5.  デバイスが低電力状態に移行すると、フレームワークは、ウェイクアップ対応の割り込みに対して[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)を呼び出しません。 このフレームワークは、ドライバーによって提供されている場合、 [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)を呼び出します。
6.  デバイスがウェイクアップ割り込みを通知すると、フレームワークはドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックルーチンを呼び出します。
7.  ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックから成功が返された場合、フレームワークは、パッシブレベルでドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバックを呼び出します。 割り込みハンドラーが戻る前に、割り込みコントローラーの割り込みを無音にする必要があります。 ドライバーが*EvtDeviceD0Entry*からエラーコードを返した場合、フレームワークは割り込みを切断し、ドライバーが指定している場合はドライバーの[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバックを呼び出します。
8.  次のウェイクアップイベントコールバックルーチンが、ドライバーによって提供されている場合、フレームワークはを呼び出します。
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)

9.  フレームワークは、「[関数またはフィルタードライバーの電源投入シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)」で説明されているように、通常の電源投入コールバックシーケンスを続行します。

[ **! Wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt)デバッガー拡張機能を使用すると、特定の割り込みがウェイクアップに対応するように構成されているかどうかを確認できます。

Wake 割り込み機能は、USB のセレクティブサスペンドと組み合わせて使用することはできません。

 

 





