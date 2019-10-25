---
title: システム ウェイクアップのサポート
description: システム ウェイクアップのサポート
ms.assetid: 519dcd1a-9975-48b1-a032-04348b903ac5
keywords:
- システムウェイクアップ WDK KMDF
- 電源管理 WDK KMDF、ウェイクアップ機能
- ウェイクアップ機能 WDK KMDF
- スリープ電源管理 WDK KMDF
- 低電力状態 WDK KMDF
- 電源管理イベントの WDK KMDF
- PME WDK KMDF
- 電源管理機能 WDK KMDF
- PMC WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5277869903b6ea95c1101d9e50cddbfdf0ff288e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831689"
---
# <a name="supporting-system-wake-up"></a>システム ウェイクアップのサポート


システムが低電力状態にある間、一部のデバイスでは、受信ネットワークパケットなどの外部イベントを検出し、システムをスリープ解除できます。 たとえば、デバイスの電源管理機能 (PMC) の登録に示されているように、PCI デバイスにシステムウェイクアップ機能がある場合、PCI バスの電源管理イベント (PME) シグナルを発生させてシステムをスリープ解除します。

デバイスがシステム全体の低電力状態からシステムをウェイクアップできる場合、[電源ポリシー所有者](power-policy-ownership.md)の[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、次の2つの手順を実行する必要があります。

1.  [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)を呼び出して、以下を指定します。

    -   デバイスが入力する低電力状態
    -   ユーザーがデバイスのアイドル設定を制御できるかどうか
    -   デバイスのウェイク機能が有効か無効か

    これらの設定の詳細については、「 [**WDF\_DEVICE\_POWER\_POLICY\_WAKE\_settings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体」を参照してください。

2.  [**Wdfdeviceinitsetpowerpolicyeventcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)を呼び出して、デバイスに必要な場合は、次のイベントコールバック関数を登録します。
    -   [*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)または[*EvtDeviceArmWakeFromSxWithReason*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)。これにより、デバイスのハードウェアが外部のウェイクアップイベントに応答できるようになります。
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)。これにより、デバイスが外部ウェイクアップイベントに応答する機能が無効になります。
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)。バスがウェイクアップ信号を検出したことをドライバーに通知します。

バスドライバーは、システムのウェイクアップにも参加します。 通常、デバイスのバスのドライバーには、 [*EvtDeviceEnableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)と[*EvtDeviceDisableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)のコールバック関数が用意されています。 これらの関数は、低電力状態から復帰するデバイスの機能を有効または無効にするために、バスアダプターで必要な操作を実行します。

バスドライバーは、デバイスがウェイクアップ信号をトリガーしたと判断した場合、デバイスの電源を復元する必要があることをフレームワークに通知するために、 [**WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)を呼び出す必要があります。 次に、フレームワークはこの情報をドライバースタック内の残りのドライバーに渡します。

デバイスのウェイクアップ機能を制御するレジストリエントリの詳細については、「ユーザーによる[デバイスのアイドル状態とウェイク動作の制御](user-control-of-device-idle-and-wake-behavior.md)」を参照してください。

 

 





