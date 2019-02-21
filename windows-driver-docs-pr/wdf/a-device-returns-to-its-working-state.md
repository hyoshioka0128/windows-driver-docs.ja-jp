---
title: デバイスは、作業の状態に戻ります
description: デバイスは、作業の状態に戻ります
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- デバイスの電源状態が WDK KMDF
- 作業状態 WDK KMDF
- 電源状態が WDK KMDF
- システム ウェイク アップ WDK KMDF
- 電源管理 WDK KMDF、ウェイク アップ機能
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce525cafebccd00971426e0ebfdcf7ea5cd58287
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539689"
---
# <a name="a-device-returns-to-its-working-state"></a>デバイスは、作業の状態に戻ります


低電力状態にあるデバイスは、次のいずれかが発生した場合の稼働状態に返されます。

-   デバイスは、外部イベントを検出し、そのバス上ウェイク信号をトリガーします。 ウェイク信号の呼び出しを検出するバス ドライバー [ **WdfDeviceIndicateWakeStatus**](https://msdn.microsoft.com/library/windows/hardware/ff546025)します。 結果として、フレームワークが、バス ドライバーの[ *EvtDeviceDisableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540858)コールバック関数。

-   デバイスがアイドル状態だったし、ドライバーは呼び出し[ **WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)します。

-   システムの電源の状態は、低電力状態からの作業 (S0) 状態に変更されました。

フレームワークが、バス ドライバーをこのような状況の各に[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数は、作業 (D0) の状態 (バスの子デバイス) のデバイスを復元します。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848) (存在する) 場合、コールバック関数。

2.  フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)コールバック関数 (存在する) 場合の各中断し、呼び出し、ドライバーの[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)コールバック関数 (存在する) 場合、ドライバーには、デバイスの割り込みが有効にすることができます。

3.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerFill*](https://msdn.microsoft.com/library/windows/hardware/ff540932)、 [ *EvtDmaEnablerEnable*](https://msdn.microsoft.com/library/windows/hardware/ff540929)と[ *EvtDmaEnablerSelfManagedIoStart* ](https://msdn.microsoft.com/library/windows/hardware/ff541663)コールバックが作成された DMA チャネルごと (存在する) 場合に機能します。

4.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ *EvtDeviceDisarmWakeFromS0* ](https://msdn.microsoft.com/library/windows/hardware/ff540860)または[ *EvtDeviceDisarmWakeFromSx* ](https://msdn.microsoft.com/library/windows/hardware/ff540862)コールバック関数。

5.  フレームワークは、ドライバーの[ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838) (存在する) 場合、コールバック関数。

6.  フレームワークの再起動のすべてのドライバーの電源管理対象の I/O キューと呼び出しの[ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)コールバック関数 (必要な場合)。

7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff540905)コールバック関数。

 

 





