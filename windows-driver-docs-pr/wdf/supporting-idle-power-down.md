---
title: アイドル電源切断のサポート
description: 一部のデバイスは、システムが動作中 (S0) 状態になっている間は、低電力 (Dx) 状態になることがあります。
ms.assetid: d0ce51db-eeb7-45ef-b823-248cd03ee2a9
keywords:
- アイドル状態の電源ダウン WDK KMDF
- 電源管理 WDK KMDF、アイドル電力ダウン
- ウェイクアップ機能 WDK KMDF
- スリープ電源管理 WDK KMDF
- 低電力状態 WDK KMDF
- システムのスリープ状態 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7c792e5a00a79e2fb69531ba45cabffecb5d558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831789"
---
# <a name="supporting-idle-power-down"></a>アイドル電源切断のサポート


一部のデバイスは、システムが動作中 (S0) 状態になっている間は、低電力 (Dx) 状態になることがあります。 Windows 8 以降では、デバイスは、Dx 状態を入力する前に、低電力機能電源状態 (Fx) に移行できます。 このようなデバイスでは、デバイスがアイドル状態 (使用されていない) になると、事前に決められた時間が経過すると、デバイスまたはコンポーネントの機能が低下します。

これらのデバイスの中には、外部イベントを検出したときにバスでウェイクアップ信号をトリガーするものもあります。 バスドライバーはこの信号に応答し、ドライバースタックはデバイスを動作状態に復元します。 (外部イベントを検出しないデバイスは、その動作状態へのデバイスの復元を開始するようにバスドライバーに指示されるまで、低電力状態のままになります)。

デバイスまたはコンポーネントがアイドル状態のときに電源を切ることができる場合、[電源ポリシー所有者](power-policy-ownership.md)の[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、次の2つの手順を実行する必要があります。

1.  [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出して、以下を指定します。

    -   デバイスが入力する低電力状態
    -   デバイスがアイドル状態の[まま](#idle-conditions)になってから電力状態が減少するまでの時間
    -   デバイスが外部イベントを検出し、バスでウェイクアップシグナルをトリガーできるかどうか
    -   ユーザーがデバイスのアイドル設定を制御できるかどうか
    -   デバイスのアイドル状態の電源をオンまたはオフにするかどうか
    -   システムが動作中 (S0) 状態に戻ったときに、デバイスが動作中 (D0) 状態に戻るかどうか
    -   デバイスのアイドルタイムアウト値が電源管理フレームワーク (PoFx) によって決定されるかどうか
    -   アイドルタイムアウト期間が経過したときに、フレームワークがデバイスを D3cold の電源状態にするかどうか

    これらの設定の詳細については、「 [**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)の構造」を参照してください。また、[機能力の状態もサポート](supporting-functional-power-states.md)しています。

2.  [**Wdfdeviceinitsetpowerpolicyeventcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)を呼び出して、デバイスに必要な場合は、次のイベントコールバック関数を登録します。
    -   [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)(バスではなく) デバイスハードウェアが外部ウェイクアップイベントに応答できるようにします。
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0): 外部のウェイクアップイベントに応答するための (バスの機能ではなく) デバイスの能力を無効にします。
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)。バスがウェイクアップ信号を検出したことをドライバーに通知します。


## <a name="idle-conditions"></a>アイドル状態

次のすべての条件が満たされると、フレームワークはデバイスがアイドル状態であると見なし、アイドル時間のカウントを開始します。

-   このデバイスインスタンスに対して作成された電源管理キューには、キューで待機しているかドライバーにディスパッチされた要求がありません。 要求がドライバーにディスパッチされ、ドライバーから i/o ターゲットに送信された場合、要求はまだキューに関連付けられています。 ドライバーが要求を送信するために [[**送信] と [破棄] オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_forward_options_flags)を使用していない限り、デバイスはアイドル状態とは見なされません。 非電力管理キュー内の要求は、デバイスがアイドル状態になるまでカウントされません。
-   以前に[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)というドライバーが呼び出された場合、ドライバーは[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)という名前になります。
-   電源ポリシーの所有者がバスドライバーの場合、バスドライバーの子デバイスはいずれも D0 にありません。

お使いのデバイスでドライバー (またはユーザー) がアイドル状態の電源を入れている場合は、 [**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)メソッドを使用しなければならないことがあります。 デバイスが動作中 (D0) 状態の場合、このメソッドは、ドライバーが[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)を呼び出すまで、デバイスのアイドル状態を防ぎます。 ドライバーが**Wdfdevicestopidle**を呼び出したときにデバイスの電力が低い状態になっていて、システムが動作している (S0) 状態になっている場合、フレームワークは、デバイスを動作中 (D0) 状態に復元するようにバスドライバーに要求します。 **Wdfdevicestopidle**を正常に呼び出すたびに、 **WdfDeviceResumeIdle**の呼び出しで一致する必要があります。 デバッガーでの power reference のカウントの表示については、「 [WDF での電源参照のリークのデバッグ](debugging-power-reference-leaks-in-wdf.md)」を参照してください。

ドライバーが[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出す必要がある場合の詳細については、メソッドのリファレンスページを参照してください。

デバイスを低電力状態からスリープ解除できる場合、デバイスのバスのドライバーはデバイスのスリープ解除に参加します。 バスドライバーは、通常、 [*EvtDeviceEnableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)および[*EvtDeviceDisableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)コールバック関数を提供します。 これらの関数は、低電力状態から復帰するデバイスの機能を有効または無効にするために、バスアダプターで必要な操作を実行します。

デバイスのアイドル状態を制御するレジストリエントリの詳細については、「[デバイスのアイドル状態とスリープ状態の動作のユーザー制御](user-control-of-device-idle-and-wake-behavior.md)」を参照してください。

 

 





