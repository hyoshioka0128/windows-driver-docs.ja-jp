---
title: システムのウェイク アップをサポートしています。
description: システムのウェイク アップをサポートしています。
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
ms.openlocfilehash: 770e61d38caa0d308537ef770bb83217b355afef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528879"
---
# <a name="supporting-system-wake-up"></a>システムのウェイク アップをサポートしています。


システムは、低電力状態では、一部のデバイスは、受信ネットワーク パケットなどの外部イベントを検出し、システムのスリープ状態を解除できます。 たとえば、PCI デバイスがシステムのウェイク アップ機能では、デバイスの電源管理機能 (PMC) の登録に記載されているスリープ状態をシステム PCI バス上の電源管理イベント (PME) シグナルを発生させることで。

デバイスは、システム、システム全体の低電力状態からスリープ解除できる場合、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)でコールバック関数、[電源ポリシー所有者](power-policy-ownership.md)を実行する必要があります、次の 2 つの手順。

1.  呼び出す[ **WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909)を指定します。

    -   デバイスが入力する低電力状態
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   デバイスのウェイク アップ機能を有効または無効にするかどうか

    これらの設定の詳細については、次を参照してください。、 [ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551277)構造体。

2.  呼び出す[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)デバイスの必要な場合は、次のイベントのコールバック関数を登録します。
    -   [*EvtDeviceArmWakeFromSx* ](https://msdn.microsoft.com/library/windows/hardware/ff540844)または[ *EvtDeviceArmWakeFromSxWithReason*](https://msdn.microsoft.com/library/windows/hardware/ff540846)、ウェイク アップの外部イベントに応答するデバイスのハードウェアを有効にします。
    -   [*EvtDeviceDisarmWakeFromSx*](https://msdn.microsoft.com/library/windows/hardware/ff540862)、ウェイク アップの外部イベントに応答するデバイスの機能を無効にします。
    -   [*EvtDeviceWakeFromSxTriggered*](https://msdn.microsoft.com/library/windows/hardware/ff540923)バスがウェイク信号を検出、ドライバーに通知します。

バス ドライバーは、ウェイク アップするシステムにも参加します。 デバイスのバスのドライバーは、通常は[ *EvtDeviceEnableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540866)と[ *EvtDeviceDisableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540858)コールバック関数。 これらの関数は、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

呼び出す必要があります、バス ドライバーでは、デバイスがウェイク信号をトリガーしたことを判断、 [ **WdfDeviceIndicateWakeStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff546025)デバイスの電源を復元することをフレームワークに通知するためにします。 フレームワークは、この情報をドライバー、ドライバー スタック内の残りの部分に渡します。

デバイスのウェイク アップ機能を制御するレジストリ エントリについては、[ユーザー コントロールのデバイスがアイドル状態と動作のスリープ解除](user-control-of-device-idle-and-wake-behavior.md)を参照してください。

 

 





