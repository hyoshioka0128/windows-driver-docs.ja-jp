---
title: 複数コンポーネント デバイスでのアイドル電源切断のサポート
description: 複数コンポーネント デバイスでのアイドル電源切断のサポート
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9632e4c16702fad90d759cff22beb0aa3c35eac8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384275"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>複数コンポーネント デバイスでのアイドル電源切断のサポート


\[KMDF にのみ適用されます。\]

複数コンポーネントのデバイスの KMDF ドライバーがサポートできる[アイドル状態の電源切断](supporting-idle-power-down.md)と機能の電力状態。 ここで、ドライバーは、電源管理フレームワーク (PoFx) を直接登録をするためですドライバー PoFx と結果として得られる Dx 状態変更について調整する必要があります。

## <a name="providing-device-power-policy-idle-settings"></a>デバイスの電源ポリシーのアイドル状態の設定を提供します。


呼び出し時に[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)、ドライバーを設定する必要があります**IdleTimeoutType**に**DriverManagedIdleTimeout**で、[ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体。 さらに、ドライバーを設定する必要があります**PowerUpIdleDeviceOnSystemWake**に**WdfTrue**、および**IdleCaps**に[ **IdleCannotWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ne-wdfdevice-_wdf_power_policy_s0_idle_capabilities)次の例のようにします。

```ManagedCPlusPlus
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS s0IdleSettings;

WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&s0IdleSettings, 
                                           IdleCannotWakeFromS0);
s0IdleSettings.IdleTimeoutType = DriverManagedIdleTimeout;
s0IdleSettings.PowerUpIdleDeviceOnSystemWake = WdfTrue;
s0IdleSettings.IdleTimeout = 1;
status = WdfDeviceAssignS0IdleSettings(device, &s0IdleSettings);
```

## <a name="transitioning-from-working-d0-to-low-power-dx-state"></a>省電力 (Dx) の状態 (D0) の作業から移行


[ *EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)、ドライバー呼び出し[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)から WDF の防止、電源の参照を実行するには低電力状態には、デバイスを配置することです。

ドライバーでは、電源の参照を解放呼び出して[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)からその[ *DevicePowerRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)コールバックルーチンです。

WDF が電源のすべての参照がリリースされた後すぐに低電力状態にデバイスを配置するため、ドライバーは通常は非常に短いアイドル タイムアウトを指定します。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>省電力 (Dx) から (D0) の操作の状態に移行


[ *DevicePowerRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)ドライバーの作業 (D0) 状態にデバイスを表示する必要があります。 これを行うにする必要がありますに延期ワーカー スレッドへの呼び出し[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)で、 *WaitForD0*パラメーターが TRUE に設定します。 このブロッキング呼び出し**WdfDeviceStopIdle**する必要があります*を確立できません*内から*DevicePowerRequiredCallback*します。

代わりに、ドライバーがパッシブのレベルで実行しているし、はしないように保証するワーカー スレッドをブロックしている呼び出しを延期する必要があります、 [ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)電源管理対象のキューの I/O のコンテキストでを呼び出すルーチンをディスパッチします。

ドライバーが呼び出されていた場合[ **WdfDeviceInitSetPowerPageable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)ドライバーを呼び出すことができます (つまり、電源の遷移中にページング可能なデータにアクセスできる)、 [ **WdfWorkItemCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)フレームワークの作業項目を作成します。 ドライバーが設定されていない電源ページング可能な場合、ドライバーは、独自のシステム スレッドを作成する必要があります。 詳細については、次を参照してください。 [ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)します。

後[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)メソッドでエラーが返されます場合でも、取得、ドライバーを呼び出す必要があります[ **PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)します。

 

 





