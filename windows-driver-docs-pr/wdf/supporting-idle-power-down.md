---
title: アイドル電源切断のサポート
description: 一部のデバイスは、システムでの作業 (S0) 状態のまま、低電力状態に (Dx) を入力できます。
ms.assetid: d0ce51db-eeb7-45ef-b823-248cd03ee2a9
keywords:
- アイドル状態の電源切断 WDK KMDF
- 電源管理 WDK KMDF、アイドル状態の電源切断
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- 低電力状態 WDK KMDF
- システム スリープ WDK KMDF を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffcf563c40650162a94c2e931825ce4d97c13f3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572780"
---
# <a name="supporting-idle-power-down"></a>アイドル電源切断のサポート


一部のデバイスは、システムでの作業 (S0) 状態のまま、低電力状態に (Dx) を入力できます。 Windows 8 以降、デバイスに移行する省電力機能の電源の状態 ([fx]) Dx 状態を入力する前にします。 このようなデバイスでは、フレームワークを開始するデバイスやコンポーネントの機能を削減後、デバイスがアイドル状態 (未使用) の事前に定義された (および設定可能な) 時間に対して。

外部イベントを検出すると、バスのウェイク アップの信号をトリガーこれらのデバイスのこともできます。 バス ドライバーが、このシグナルに応答し、ドライバー スタック、デバイスを動作状態に復元します。 (外部イベントを検出しないデバイスまで低電力状態でフレームワークを稼働状態に、デバイスの復元を開始するバス ドライバーの確認です。)

場合は、デバイスやコンポーネント電源を切断できますアイドル状態のとき、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)でコールバック関数、[電源ポリシー所有者](power-policy-ownership.md)次の 2 つを実行する必要があります手順:

1.  呼び出す[ **WdfDeviceAssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545903)を指定します。

    -   デバイスが入力する低電力状態
    -   時間の長さですが、デバイス[アイドル状態を維持する必要があります](#idle-conditions)の電源状態が低くしたりする前に
    -   デバイスの外部のイベントの検出し、バスのウェイク アップの信号をトリガーできるかどうか
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   アイドル状態のデバイスの電源機能を有効または無効にするかどうか
    -   作業 (S0) 状態に戻ると、システムにデバイスが作業 (D0) 状態に戻すかどうか
    -   電源管理フレームワーク (PoFx) によって、デバイスのアイドル タイムアウト値を判断するかどうか
    -   かどうか、フレームワークに配置できますデバイス D3cold 電源の状態、アイドル タイムアウト期間が切れるときに

    これらの設定の詳細については、次を参照してください、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551270)構造として。としても[サポート機能の電力状態](supporting-functional-power-states.md)します。

2.  呼び出す[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)デバイスの必要な場合は、次のイベントのコールバック関数を登録します。
    -   [*EvtDeviceArmWakeFromS0*](https://msdn.microsoft.com/library/windows/hardware/ff540843)、ウェイク アップの外部イベントに応答するデバイスのハードウェア (バスではない) ことができます
    -   [*EvtDeviceDisarmWakeFromS0*](https://msdn.microsoft.com/library/windows/hardware/ff540860)、ウェイク アップの外部イベントに応答するデバイスの機能 (バスの機能ではない) を無効にします
    -   [*EvtDeviceWakeFromS0Triggered*](https://msdn.microsoft.com/library/windows/hardware/ff540919)バスがウェイク信号を検出、ドライバーに通知します。




フレームワークは、アイドル状態になるデバイスを考慮しの次の条件がすべて満たされたときに、アイドル時間をカウントします。

-   このデバイス インスタンス用に作成された電源管理対象のキューのいずれも任意の要求をキューで待機しているまたはドライバーにディスパッチします。 場合は、要求は、ドライバーにディスパッチされましたが、ドライバーが I/O のターゲットに送信、要求がキューにも関連します。 デバイスは反映されませんアイドル状態で、ドライバーが使用されていない場合、 [**送信し、オプションを忘れた**](https://msdn.microsoft.com/library/windows/hardware/ff552462)要求を送信します。 電源非管理対象のキュー内の要求はカウントされませんデバイスに向けたアイドル状態。
-   ドライバーと呼ばれていた場合[ **WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)、ドライバーは、その後、呼び出されて[ **WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)します。
-   電源ポリシーの所有者がバス ドライバーの場合は、D0 ではありません、バス ドライバーの子デバイスです。

場合は、ドライバー (またはユーザー) には、アイドル状態に、デバイスの電源オフができますが、使用する必要があります、 [ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)メソッド。 デバイスがその動作 (D0) 状態の場合は、このメソッドは、ドライバー呼び出されるまでアイドル状態から、デバイスを防ぎます[ **WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)します。 ドライバーを呼び出すときに、デバイスが省電力状態がかどうか**WdfDeviceStopIdle**フレームワークがデバイスの作業 (D0) 状態を復元するバス ドライバーを要求、システムが作業 (S0) の状態である場合と。 すべての成功した呼び出し**WdfDeviceStopIdle**への呼び出しで一致する必要があります**WdfDeviceResumeIdle**します。 デバッガーで電源の参照カウントを表示する方法については、[WDF を使用した Power 参照リークのデバッグ](debugging-power-reference-leaks-in-wdf.md)を参照してください。

詳細については、ドライバーが呼び出す必要があります[ **WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)メソッドのリファレンス ページを参照してください。

低電力状態からスリープ解除できるデバイスの場合、デバイスのバスのドライバーは、デバイスの起動時に参加します。 バス ドライバーは、通常は[ *EvtDeviceEnableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540866)と[ *EvtDeviceDisableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540858)コールバック関数。 これらの関数は、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

デバイスのアイドル状態の機能を制御するレジストリ エントリについては、[ユーザー コントロールのデバイス アイドル状態と動作のスリープ解除](user-control-of-device-idle-and-wake-behavior.md)を参照してください。

 

 





