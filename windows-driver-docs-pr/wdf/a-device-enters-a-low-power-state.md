---
title: デバイスが省電力状態に入る
description: デバイスが省電力状態に入る
ms.assetid: 07d7c460-4316-40a9-b502-f7c1bd1182c2
keywords:
- 電源管理 WDK KMDF、低電力状態
- 低電力状態 WDK KMDF
- 電源状態が WDK KMDF
- デバイスの電源状態が WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- アイドル状態の電源切断 WDK KMDF
- 電源管理 WDK KMDF、アイドル状態の電源切断
- システム スリープ WDK KMDF を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2047a746c6366da0ad7527b73bb9a7f14b76cccf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559200"
---
# <a name="a-device-enters-a-low-power-state"></a>デバイスが省電力状態に入る


デバイスは、その動作 (D0) 状態のままし、次のいずれかが発生した場合は低電力状態になります。

-   デバイスがアイドル状態 (にアクセスしていない) のシステムでの作業 (S0) 状態のまま、低電力アイドル状態を入力することができます。

-   システムの電源の状態は、低電力状態にその動作 (S0) 状態から変更されました。 (ドライバーを呼び出すことができます[ **WdfDeviceGetSystemPowerAction** ](https://msdn.microsoft.com/library/windows/hardware/ff546022)システムの電源の状態が変更された理由を特定します)。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最上位である driver 以降では、シーケンスで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)コールバック関数。

2.  フレームワークは、ドライバーの呼び出しや I/O キューの電源管理対象のすべてを停止、 [ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)コールバック関数 (存在する場合)。

3.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ *EvtDeviceArmWakeFromS0*](https://msdn.microsoft.com/library/windows/hardware/ff540843)、 [ *EvtDeviceArmWakeFromSx* ](https://msdn.microsoft.com/library/windows/hardware/ff540844)、または[ *EvtDeviceArmWakeFromSxWithReason* ](https://msdn.microsoft.com/library/windows/hardware/ff540846)コールバック関数。

4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)、 [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)、および[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)作成 DMA チャネルごと (存在する) 場合にコールバックが機能します。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)コールバック関数 (存在する) 場合、し、呼び出し、ドライバーの[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック関数 (存在する) 場合、各割り込みのドライバーは、デバイスの割り込みを無効にできます。

6.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855) (存在する) 場合、コールバック関数。

バス ドライバーは、最後に呼び出されるスタックのドライバーです。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)低電力状態にコールバック関数では、コールバック関数の設定 (バスの子デバイス) のデバイスの電源の状態。 フレームワークは、電源ポリシーの所有者が別の低電力状態を指定しない限り、D3 低電力状態を指定します。

 

 





