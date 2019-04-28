---
title: PnP マネージャーがシステム リソースを再配布する
description: PnP マネージャーがシステム リソースを再配布する
ms.assetid: fc88ae0a-5b78-4292-a101-29d2fc383555
keywords:
- PnP WDK KMDF、リソースの再配布
- プラグ アンド プレイ WDK KMDF、リソースの再配布
- リソースの再配布 WDK KMDF
- WDK KMDF のリソースを再配布
- 電源シーケンス WDK KMDF
- 電源投入シーケンス WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d0d32b15026e06fb741a36e6dd87f122e892d0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377412"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP マネージャーがシステム リソースを再配布する


ユーザーがシステムでは、デバイスを追加し、PnP マネージャーが別のデバイスに既に割り当てられているシステム リソースがデバイスに必要な場合、PnP マネージャーは、リソースを再割り当てを試みます。

このプロセス中には、PnP マネージャーは、デバイスを停止し、外の作業 (D0) 状態に移動します。 提供新しいリソースの一覧をデバイスに新しいリソースを使用して、再起動ができるようにします。

リソースを再頒布時に PnP マネージャーは変更されません、デバイスのリソースの割り当てがある、デバイスのドライバーのいずれかの場合。

-   呼ばれる[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)特別なファイルは、デバイスで開いているとします。

-   呼ばれる[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)します。

-   指定された、 [ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)コールバック関数、およびコールバック関数を再割り当てが拒否しました。

### <a name="power-down-sequence"></a>シーケンスを電源

各関数とフィルター ドライバーを停止中でデバイスをサポートするために、フレームワークはシーケンス、ドライバー スタックの最上位である driver 以降では、一度に 1 つのドライバーで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)コールバック関数。

2.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを停止します。

3.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)、 [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)、および[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)作成された DMA チャネルごとのコールバック関数。

4.  ドライバーの呼び出す[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)と[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック関数 (存在する場合)ドライバーは、デバイスの割り込みを無効にできます。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855) (存在する) 場合、コールバック関数。

6.  フレームワークは、ドライバーの[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

バス ドライバー スタックの最下位のドライバーは、最後に呼び出されます。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック関数では、デバイスの PDO を表す framework デバイス オブジェクトをハンドルを渡しますが、 *TargetState* @property **WdfPowerDeviceD3Final**します。 フレームワークを呼び出すときに、バス ドライバーを制御できますその[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数を呼び出して[  **。WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)します。

### <a name="power-up-sequence"></a>電源投入シーケンス

呼ばれる最初のドライバーは、バス ドライバーです。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数では、コールバック関数では、デバイス (バスの子デバイス) を作業 (D0) 状態に復元します。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

2.  フレームワークは、ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848) (存在する) 場合、コールバック関数。

3.  フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)と[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)コールバック関数 (存在する場合)、ドライバーがデバイスの割り込みを有効にするようにします。

4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerFill*](https://msdn.microsoft.com/library/windows/hardware/ff540932)、 [ *EvtDmaEnablerEnable*](https://msdn.microsoft.com/library/windows/hardware/ff540929)と[ *EvtDmaEnablerSelfManagedIoStart* ](https://msdn.microsoft.com/library/windows/hardware/ff541663)作成された DMA チャネルごとのコールバック関数。

5.  フレームワークは、ドライバーの[ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838) (存在する) 場合、コールバック関数。

6.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを再起動します。

7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff540905)コールバック関数。

 

 





