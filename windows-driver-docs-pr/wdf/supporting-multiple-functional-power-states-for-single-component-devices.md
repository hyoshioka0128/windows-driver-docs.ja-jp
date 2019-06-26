---
title: 単一コンポーネントのデバイス、1 つまたは複数の機能の電力状態
description: KMDF ドライバーで単一コンポーネントのデバイスの [fx] 状態のサポートを実装する方法について説明します。
ms.assetid: C7EFD71F-E101-4160-9703-E1DBD507698C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7976d6ea7f8ead2fb9570a70f2559719d165bd2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368076"
---
# <a name="supporting-single-component-devices-with-single-or-multiple-functional-power-states"></a>1 つまたは複数の機能電源状態を持つ単一コンポーネント デバイスのサポート


単一コンポーネントのデバイスの KMDF ドライバーは、コンポーネントの 1 つまたは複数の機能の電源状態を定義および電源管理フレームワーク (PoFx) がコンポーネントの [fx] 状態が変更されたときに呼び出すコールバック機能またはのアクティブまたはアイドル状態を登録できます。変更します。 単一コンポーネントのデバイスの UMDF ドライバーは、UMDF バージョン 2.0 以降、機能の 1 つの電源の状態 (F0) を定義できます。

PoFx の詳細については、次を参照してください。 [、電源管理フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)します。

単一コンポーネントのデバイスの [fx] 状態のサポートを実装する前に注文では、次を行う必要があります。 または最初の期間中にデバイスが起動します。

1.  この手順は、KMDF ドライバーのみです。 呼び出す[ **WdfDeviceWdmAssignPowerFrameworkSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings) PoFx で登録するときに WDF を使用して電源フレームワークの設定を指定します。 [ **WDF\_POWER\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)を呼び出すときに、ドライバーが提供する構造体**WdfDeviceWdmAssignPowerFrameworkSettings**ドライバーは、いくつかのコールバック関数へのポインターを提供できます。 ドライバーは、機能の 1 つの電源状態 (F0) のみをサポートする場合は、この手順を省略できます。
2.  この手順は、KMDF ドライバーおよび UMDF ドライバーに適用されます。 呼び出す[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)設定と、 **IdleTimeoutType**のフィールド、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体を**SystemManagedIdleTimeout**または**SystemManagedIdleTimeoutWithHint**します。 使用すると、WDF PoFx に登録します。

    PoFx に登録するときに、KMDF ドライバー、フレームワークは、ドライバーがで提供される情報を使用して[ **WDF\_POWER\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)とき呼び出された[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)します。

デバイスを複数回起動できる、ため、たとえばリソースが再調整が発生した場合、ドライバーを実行内で、前の手順、 [ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数。 ドライバーが登録されている場合、 *EvtDeviceSelfManagedIoInit*コールバック関数では、フレームワークは呼び出し 1 回を各デバイスでは、フレームワークには、ドライバーが呼び出された後[ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)初めて用コールバック関数。

このトピックの情報の残りの部分は、KMDF ドライバーにのみ適用されます。

## <a name="powering-up"></a>電源を入れる


ドライバーを呼び出すと[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)へのポインターを提供できる、 [ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバック関数。

フレームワークは、ドライバーの[ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) PoFx がフレームワークに登録した後、コールバック関数。 通常の電源投入シーケンスの例を次に示します。

1.  [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
2.  [*EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (*PrevState* = **WdfPowerDeviceD3Final**)
3.  [*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)
4.  [*EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) /PoFx ハンドルが使用可能な/

ドライバーの提供、 [ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバックの場合は、POHANDLE を使用して power framework 登録の追加の操作を実行する必要があります。 待機時間を指定、たとえば、保存場所、およびウェイク要件。 POHANDLE を使用するルーチンの詳細については、次を参照してください。[デバイスの電源管理ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ドライバーは、POHANDLE を使用しても PoFx で電源制御要求の交換します。

-   ドライバーに PoFx を電源制御要求を送信するには、 [ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)コールバック関数、および、使用する呼び出しの結果として得られる POHANDLE [ **PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)します。
-   PoFx によって要求された電源管理操作を実行する、ドライバーには、 [ *PowerControlCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_power_control_callback)コールバック ルーチンでその[ **WDF\_POWER\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)構造体。

## <a name="powering-down"></a>電源


WDF の呼び出し、 [ *EvtDeviceWdmPrePoFxUnregisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_pre_po_fx_unregister_device) PoFx で指定した登録を削除する前に、コールバック関数。

ドライバーへのポインターを提供できる、 [ *ComponentIdleStateCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)で日常的な[ **WDF\_POWER\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)に提供される構造[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)します。 PoFx では、指定したコンポーネントの電源状態の [fx] に変更が保留中のドライバーに通知するには、このルーチンを呼び出します。 このコールバック ルーチンで、ドライバーは、機能の状態の変更に関連するハードウェア固有の操作を実行できます。

たとえば、低電力状態に [fx] に、コンポーネントを移行する前にドライバー可能性がありますハードウェアの状態を保存し、割り込みと DMA を無効にします。 ドライバー呼び出し[ **WdfInterruptReportInactive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)割り込みがアクティブでなくなったことをシステムに通知します。 F 状態遷移中に、割り込みをオフにすると、全体的なシステムの電力消費量を減らすことができます。

ドライバーへのポインターを指定できますも、 [ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)で日常的な[ **WDF\_POWER\_FRAMEWORK\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)構造体。 PoFx では、コンポーネントがアイドル状態になることをドライバーに通知するには、このルーチンを呼び出します。 このルーチンでは、ドライバーは、その電源管理対象のキューおよび自己管理型の I/O 操作を停止するプロセスを開始します。

1.  呼び出す[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)デバイスの電源管理対象のキューごとに 1 回です。 呼び出すたびに**WdfIoQueueStop**指定、 [ *EvtIoQueueState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)コールバック。 ドライバーの呼び出しでは通常、 **WdfIoQueueStop**内から[ *ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)します。
2.  各電源管理対象のキューからドライバーにディスパッチされる要求が迅速に完了したことを確認します。 ドライバーによって、次の一部またはすべてがあります。
    -   ドライバーが長時間にわたって要求を保持しない処理を行っている I/O ターゲットに転送しない場合は、手順 3 に進みます。
    -   ドライバーは、長時間にわたって特定の要求を保持している場合は、手動のキューにこれらの要求をもう一度キューします。 その[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback) 、日常的なドライバーが取得要求。
    -   ドライバーは、それらを長時間にわたって保持する I/O ターゲットを特定の要求を転送する場合は、これらの要求をキャンセルします。 内の要求を再送信[ *ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)します。

3.  各キューを停止すると、フレームワーク[ *EvtIoQueueState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)します。 ドライバーが複数の電源管理対象のキューを停止している場合、フレームワーク*EvtIoQueueState*複数回、1 回キューごとにします。

    ドライバーを呼び出す必要があります[ **PoFxCompleteIdleCondition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlecondition)最後後[ *EvtIoQueueState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)関数が呼び出されました。 たとえば、ドライバーは、この呼び出しは、過去から*EvtIoQueueState*します。

    どの呼び出しが最後で判断するために、ドライバーは、フレームワークと呼ばれる回数を追跡するカウンターを使用可能性があります[ *EvtIoQueueState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)します。 Singlecomp サンプルでは、この方法を示します。 このサンプルは、以降、Windows 8 WDK で使用できます。

一般的な電源オフ手順の例を次に示します。

1.  [*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)
2.  [*ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)
3.  [*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)
4.  [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)

電源管理対象のキューおよび自己管理型の I/O 操作での再起動[ *ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)します。

ドライバーと呼ばれていた場合[ **WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)、呼び出すことによって非アクティブな割り込みを再度有効にする[ **WdfInterruptReportActive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)いずれかから[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)または[ *ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)します。

 

 





