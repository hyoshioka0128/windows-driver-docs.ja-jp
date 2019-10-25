---
title: 単一コンポーネントデバイス、1つまたは複数の機能力状態
description: KMDF ドライバーの単一コンポーネントデバイスの Fx 状態サポートを実装する方法について説明します。
ms.assetid: C7EFD71F-E101-4160-9703-E1DBD507698C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed680ef6663b8feb93f9cca79c7a20a02fa530c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831737"
---
# <a name="supporting-single-component-devices-with-single-or-multiple-functional-power-states"></a>1 つまたは複数の機能電源状態を持つ単一コンポーネント デバイスのサポート


単一コンポーネントデバイス用の KMDF ドライバーでは、コンポーネントの機能の電源状態を1つ以上定義し、コンポーネントの Fx 状態が変更されたとき、またはそのアクティブ/アイドル状態になったときに、電源管理フレームワーク (PoFx) が呼び出すコールバック関数を登録できます。変化. UMDF バージョン2.0 以降では、単一コンポーネントデバイス用の UMDF ドライバーによって、単一の機能の電源状態 (F0) を定義できます。

PoFx の詳細については、「[電源管理フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)」を参照してください。

単一コンポーネントデバイスの Fx 状態サポートを実装するには、デバイスを初めて起動する前または後に、次の操作を行う必要があります。

1.  この手順は KMDF ドライバーのみを対象としています。 [**Wdfdevicewdm割り当て Powerframeworksettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)を呼び出して、pofx に登録するときに WDF が使用する power framework 設定を指定します。 [**WDF\_POWER\_FRAMEWORK の\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)の構造では、ドライバーが**Wdfdevicewdm割り当て powerframeworksettings**を呼び出すときに、ドライバーは複数のコールバック関数へのポインターを提供できます。 ドライバーが1つの機能の電源状態 (F0) のみをサポートしている場合、この手順は省略可能です。
2.  この手順は、KMDF ドライバーと UMDF ドライバーに適用されます。 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出し、 [**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体の**IdleTimeoutType**フィールドを**SystemManagedIdleTimeout**または**に設定します。SystemManagedIdleTimeoutWithHint**。 これにより、WDF が PoFx に登録されます。

    KMDF ドライバーの場合、PoFx に登録すると、フレームワークは、WDF で提供されているドライバー [ **\_POWER\_framework\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)を使用します。この情報は、 [**Wdfdevicewdm powerframeworksettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)を呼び出したときに設定されます。

デバイスは、たとえばリソースの再調整が発生した場合など、1回以上開始できるので、ドライバーは[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数内で前の手順を実行する可能性があります。 ドライバーが*Evtdeviceselfmanagedioinit*コールバック関数を登録している場合、フレームワークは最初にドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) callback 関数を呼び出した後、デバイスごとに1回呼び出します。

このトピックの残りの情報は、KMDF ドライバーにのみ適用されます。

## <a name="powering-up"></a>電源をオンにする


ドライバーが[**Wdfdevicewdm割り当て Powerframeworksettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)を呼び出すと、 [*Evtdevicewdmpostpofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバック関数へのポインターが提供されます。

フレームワークは、フレームワークが PoFx に登録された後に、ドライバーの[*Evtdevicewdmpostpofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバック関数を呼び出します。 一般的な電源オンシーケンスの例を次に示します。

1.  [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
2.  [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (*Prevstate* = **WdfPowerDeviceD3Final**)
3.  [*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)
4.  [*Evtdevicewdmpostpofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) //pofx ハンドルを使用できます

このドライバーは、power framework の登録に POHANDLE を使用して追加の操作を実行する必要がある場合に、 [*Evtdevicewdmpostpofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバックを提供します。 たとえば、待機時間、常駐状態、およびウェイクアップ要件を指定できます。 POHANDLE を使用するルーチンの詳細については、「[デバイスの電源管理ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

また、POHANDLE を使用して Pohandle と power control 要求を交換することもできます。

-   PoFx に電源管理要求を送信するために、ドライバーは[*Evtdevicewdmpostpofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバック関数を提供し、結果の pofx を使用して[**Pofxpowercontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)を呼び出します。
-   PoFx によって要求された電源管理操作を実行するために、ドライバーは、 [*Powercontrolcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_power_control_callback)コールバックルーチンを[**WDF\_power\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)構造体に提供します。

## <a name="powering-down"></a>電源を切る


WDF は、PoFx によって指定された登録を削除する前に、 [*Evtdevicewdmprepofxunregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_pre_po_fx_unregister_device)コールバック関数を呼び出します。

ドライバーは、 [**Wdfdevicewdm割り当て Powerframeworksettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)に提供する[**WDF\_POWER\_FRAMEWORK\_settings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)構造体内の[*ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)ルーチンへのポインターを提供できます。 PoFx は、このルーチンを呼び出して、指定されたコンポーネントの Fx 電源状態に対する保留中の変更をドライバーに通知します。 このコールバックルーチンでは、ドライバーは機能状態の変更に関連するハードウェア固有の操作を実行できます。

たとえば、コンポーネントを低電力の Fx 状態に移行する前に、ドライバーによってハードウェアの状態が保存され、割り込みと DMA が無効になることがあります。 ドライバーは[**WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)を呼び出して、割り込みがアクティブでなくなったことをシステムに通知します。 F 状態遷移中に割り込みをオフにすると、システム全体の電力消費が減少する可能性があります。

ドライバーは、 [**WDF\_POWER\_FRAMEWORK の\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)構造体で、 [*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)ルーチンへのポインターを提供することもできます。 PoFx は、このルーチンを呼び出して、コンポーネントがアイドル状態になったことをドライバーに通知します。 このルーチンでは、ドライバーは、電源管理キューと自己管理型の i/o 操作を停止するプロセスを開始します。

1.  各デバイスの電源管理キューに対して、 [**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)を1回呼び出します。 **Wdfioqueuestop**を呼び出すたびに、 [*Evtioqueuestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)コールバックを指定します。 通常、ドライバーは[*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)内から**Wdfioqueuestop**を呼び出します。
2.  各電源管理キューからドライバーにディスパッチされた要求が迅速に完了することを確認します。 ドライバーによっては、次の一部またはすべてが含まれる場合があります。
    -   ドライバーが長時間要求を保持しておらず、それを実行している i/o ターゲットに転送されない場合は、手順 3. に進みます。
    -   ドライバーが一定の時間内に特定の要求を保持している場合は、これらの要求を手動キューにキューへします。 [*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)ルーチンでは、ドライバーが要求を取得できます。
    -   ドライバーが特定の要求を、長時間保持する i/o ターゲットに転送する場合は、これらの要求をキャンセルします。 [*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)で要求を再送信します。

3.  各キューが停止されると、フレームワークは[*Evtioqueuestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)呼び出します。 ドライバーが複数の電源管理キューを停止している場合、フレームワークは、キューごとに1回、 *Evtioqueuestate*を複数回呼び出します。

    ドライバーは、最後の[*Evtioqueuestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)関数が呼び出された後に[**PoFxCompleteIdleCondition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlecondition)を呼び出す必要があります。 たとえば、ドライバーは、最後の*Evtioqueuestate*この呼び出しを行うことができます。

    どの呼び出しが最後であるかを判断するために、ドライバーはカウンターを使用して、フレームワークが[*Evtioqueuestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)呼び出した回数を追跡する場合があります。 Singlecomp サンプルは、この手法を示しています。 このサンプルは、Windows 8 WDK 以降で使用できます。

一般的な電源ダウンシーケンスの例を次に示します。

1.  [*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)
2.  [*ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)
3.  [*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)
4.  [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)

[*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)で、電源管理キューと自己管理型 i/o 操作を再起動します。

ドライバーが以前に[**WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)を呼び出した場合は、 [*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)または[*ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)から[**WdfInterruptReportActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)を呼び出して、非アクティブな割り込みを再び有効にします。

 

 





