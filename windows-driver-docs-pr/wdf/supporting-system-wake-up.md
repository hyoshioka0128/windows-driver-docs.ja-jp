---
title: システム ウェイクアップのサポート
description: システム ウェイクアップのサポート
ms.assetid: 519dcd1a-9975-48b1-a032-04348b903ac5
keywords:
- システム ウェイク アップ WDK KMDF
- 電源管理 WDK KMDF、ウェイク アップ機能
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- 低電力状態 WDK KMDF
- 電源管理イベントの WDK KMDF
- PME WDK KMDF
- 電源管理機能の WDK KMDF
- PMC WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0304cd242e940e01eff0122f52cb3f76b23b5c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368022"
---
# <a name="supporting-system-wake-up"></a>システム ウェイクアップのサポート


システムは、低電力状態では、一部のデバイスは、受信ネットワーク パケットなどの外部イベントを検出し、システムのスリープ状態を解除できます。 たとえば、PCI デバイスがシステムのウェイク アップ機能では、デバイスの電源管理機能 (PMC) の登録に記載されているスリープ状態をシステム PCI バス上の電源管理イベント (PME) シグナルを発生させることで。

デバイスは、システム、システム全体の低電力状態からスリープ解除できる場合、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)でコールバック関数、[電源ポリシー所有者](power-policy-ownership.md)を実行する必要があります、次の 2 つの手順。

1.  呼び出す[ **WdfDeviceAssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)を指定します。

    -   デバイスが入力する低電力状態
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   デバイスのウェイク アップ機能を有効または無効にするかどうか

    これらの設定の詳細については、次を参照してください。、 [ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体。

2.  呼び出す[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)デバイスの必要な場合は、次のイベントのコールバック関数を登録します。
    -   [*EvtDeviceArmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)または[ *EvtDeviceArmWakeFromSxWithReason*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)、ウェイク アップの外部イベントに応答するデバイスのハードウェアを有効にします。
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)、ウェイク アップの外部イベントに応答するデバイスの機能を無効にします。
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)バスがウェイク信号を検出、ドライバーに通知します。

バス ドライバーは、ウェイク アップするシステムにも参加します。 デバイスのバスのドライバーは、通常は[ *EvtDeviceEnableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)と[ *EvtDeviceDisableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)コールバック関数。 これらの関数は、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

呼び出す必要があります、バス ドライバーでは、デバイスがウェイク信号をトリガーしたことを判断、 [ **WdfDeviceIndicateWakeStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)デバイスの電源を復元することをフレームワークに通知するためにします。 フレームワークは、この情報をドライバー、ドライバー スタック内の残りの部分に渡します。

デバイスのウェイク アップ機能を制御するレジストリ エントリについては、次を参照してください。[ユーザー コントロールのデバイスがアイドル状態と動作のスリープ解除](user-control-of-device-idle-and-wake-behavior.md)します。

 

 





