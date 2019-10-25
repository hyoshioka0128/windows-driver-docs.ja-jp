---
title: 複数コンポーネント デバイスでのアイドル電源切断のサポート
description: 複数コンポーネント デバイスでのアイドル電源切断のサポート
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6b25ec8b16be38f1efef6b048b3c87000b1d5b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831785"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>複数コンポーネント デバイスでのアイドル電源切断のサポート


\[は KMDF にのみ適用され\]

複数コンポーネントのデバイス用の KMDF ドライバーは、アイドル状態の[電源](supporting-idle-power-down.md)と機能をサポートすることができます。 この場合、ドライバーは電源管理フレームワーク (PoFx) に直接登録するため、ドライバーは、結果として得られる Dx 状態の変更を PoFx で調整する必要があります。

## <a name="providing-device-power-policy-idle-settings"></a>デバイスの電源ポリシーのアイドル設定を提供する


[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出す場合、ドライバーは**IdleTimeoutType**を WDF\_\_デバイスで**DriverManagedIdleTimeout**に設定する必要があります。[**電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)データ. さらに、次の例に示すように、ドライバーは**PowerUpIdleDeviceOnSystemWake**を**wdftrue**に設定し、 **IdleCaps**を[**IdleCannotWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_power_policy_s0_idle_capabilities)に設定する必要があります。

```ManagedCPlusPlus
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS s0IdleSettings;

WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&s0IdleSettings, 
                                           IdleCannotWakeFromS0);
s0IdleSettings.IdleTimeoutType = DriverManagedIdleTimeout;
s0IdleSettings.PowerUpIdleDeviceOnSystemWake = WdfTrue;
s0IdleSettings.IdleTimeout = 1;
status = WdfDeviceAssignS0IdleSettings(device, &s0IdleSettings);
```

## <a name="transitioning-from-working-d0-to-low-power-dx-state"></a>動作中 (D0) から低電力 (Dx) 状態への移行


[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)では、ドライバーは[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出して電源参照を取得します。これにより、WDF がデバイスを低電力状態にするのを防ぐことができます。

ドライバーは、 [*Devicepowerrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)コールバックルーチンから[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)を呼び出すことによって、電源参照を解放します。

ドライバーは通常、非常に短いアイドルタイムアウトを指定します。これにより、WDF は、すべての電源参照が解放された直後にデバイスを低電力状態にします。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>低電力 (Dx) から動作 (D0) 状態への移行


[*Devicepowerrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)では、ドライバーはデバイスを動作 (D0) 状態にする必要があります。 これを行うには、 *WaitForD0*パラメーターを TRUE に設定して、ワーカースレッドに対して[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)への呼び出しを行う必要があります。 **Wdfdevicestopidle**へのこのブロッキング呼び出しは、 *Devicepowerrequiredcallback*内から作成することはでき*ません*。

代わりに、ドライバーは、パッシブレベルで実行されているワーカースレッドへのブロック呼び出しを遅延させる必要があります。これは、電源管理キューの i/o ディスパッチルーチンのコンテキストで[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)呼び出しを行わないことが保証されています。

ドライバーが以前に[**Wdfdeviceinitsetpowerpageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)を呼び出していた場合 (つまり、電源遷移中にページング可能なデータにアクセスできること)、ドライバーは[**wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)を呼び出してフレームワーク作業項目を作成できます。 ドライバーが電源のページングを設定していない場合、ドライバーは独自のシステムスレッドを作成する必要があります。 詳細については、「 [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)」を参照してください。

[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)が返された後、メソッドからエラーが返された場合でも、ドライバーは[**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出す必要があります。

 

 





