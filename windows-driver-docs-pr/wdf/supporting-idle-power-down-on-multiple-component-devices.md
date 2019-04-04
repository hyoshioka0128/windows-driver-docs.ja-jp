---
title: 複数コンポーネントのデバイスでのアイドル状態の電源のサポート
description: 複数コンポーネントのデバイスでのアイドル状態の電源のサポート
ms.assetid: 81C80E30-DAF4-4EE4-AA29-AB40A6827C26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984e23f2e2a2fc9d15d4e7b7e4105d12fb1df166
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539113"
---
# <a name="supporting-idle-power-down-on-multiple-component-devices"></a>複数コンポーネントのデバイスでのアイドル状態の電源のサポート


\[KMDF にのみ適用されます。\]

複数コンポーネントのデバイスの KMDF ドライバーがサポートできる[アイドル状態の電源切断](supporting-idle-power-down.md)と機能の電力状態。 ここで、ドライバーは、電源管理フレームワーク (PoFx) を直接登録をするためですドライバー PoFx と結果として得られる Dx 状態変更について調整する必要があります。

## <a name="providing-device-power-policy-idle-settings"></a>デバイスの電源ポリシーのアイドル状態の設定を提供します。


呼び出し時に[ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)、ドライバーを設定する必要があります**IdleTimeoutType**に**DriverManagedIdleTimeout**で、[ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551270)構造体。 さらに、ドライバーを設定する必要があります**PowerUpIdleDeviceOnSystemWake**に**WdfTrue**、および**IdleCaps**に[ **IdleCannotWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff552429)次の例のようにします。

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


[ *EvtDeviceSelfManagedIoInit*](https://msdn.microsoft.com/library/windows/hardware/ff540902)、ドライバー呼び出し[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)から WDF の防止、電源の参照を実行するには低電力状態には、デバイスを配置することです。

ドライバーでは、電源の参照を解放呼び出して[ **WdfDeviceResumeIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546838)からその[ *DevicePowerRequiredCallback* ](https://msdn.microsoft.com/library/windows/hardware/hh450949)コールバックルーチンです。

WDF が電源のすべての参照がリリースされた後すぐに低電力状態にデバイスを配置するため、ドライバーは通常は非常に短いアイドル タイムアウトを指定します。

## <a name="transitioning-from-low-power-dx-to-working-d0-state"></a>省電力 (Dx) から (D0) の操作の状態に移行


[ *DevicePowerRequiredCallback*](https://msdn.microsoft.com/library/windows/hardware/hh450949)ドライバーの作業 (D0) 状態にデバイスを表示する必要があります。 これを行うにする必要がありますに延期ワーカー スレッドへの呼び出し[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)で、 *WaitForD0*パラメーターが TRUE に設定します。 このブロッキング呼び出し**WdfDeviceStopIdle**する必要があります*を確立できません*内から*DevicePowerRequiredCallback*します。

代わりに、ドライバーがパッシブのレベルで実行しているし、はしないように保証するワーカー スレッドをブロックしている呼び出しを延期する必要があります、 [ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)電源管理対象のキューの I/O のコンテキストでを呼び出すルーチンをディスパッチします。

ドライバーが呼び出されていた場合[ **WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766)ドライバーを呼び出すことができます (つまり、電源の遷移中にページング可能なデータにアクセスできる)、 [ **WdfWorkItemCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551201)フレームワークの作業項目を作成します。 ドライバーが設定されていない電源ページング可能な場合、ドライバーは、独自のシステム スレッドを作成する必要があります。 詳細については、[ **PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)を参照してください。

後[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)メソッドでエラーが返されます場合でも、取得、ドライバーを呼び出す必要があります[ **PoFxReportDevicePoweredOn**](https://msdn.microsoft.com/library/windows/hardware/hh439526)します。

 

 





