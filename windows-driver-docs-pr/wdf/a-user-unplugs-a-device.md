---
title: ユーザーがデバイスを取り外す
description: ユーザーがデバイスを取り外す
ms.assetid: 85e69401-0128-4641-aa0f-fd7c4f22f395
keywords:
- PnP デバイスのプラグを抜くの WDK KMDF
- プラグ アンド プレイ デバイスのプラグを抜くの WDK KMDF
- 正常なデバイスの削除の WDK KMDF
- WDK KMDF のデバイスを取り外す
- デバイスの削除の WDK KMDF 驚くような
- 予期しないデバイスの削除の WDK KMDF
- WDK KMDF のデバイスを削除します。
- デバイス WDK KMDF の取り出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98662294894f1bf190168b03715465a4561f2af1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342214"
---
# <a name="a-user-unplugs-a-device"></a>ユーザーがデバイスを取り外す


ユーザーが 2 つの方法のいずれかでデバイスを削除、システムが実行中に: によって*正しく削除*ユーザーでは、システムが通知、デバイスが (たとえば、取り外しますプログラムを使用) を削除する; があることを意味するか、によって*突然の取り外し*ユーザーがシステムに通知することがなく、デバイスをコールバックすることを意味します。 バスは、突然の取り外し (USB など) をサポートする場合、デバイスのドライバーは、デバイスの急激な消滅を処理できる必要があります。

### <a href="" id="orderly-removal"></a> 所定の削除

ユーザーがデバイス マネージャーを使用して、またはプッシュして、デバイスを無効にすると、システムの取り外しますプログラムを使用して削除を要求、[フロッピー](supporting-ejectable-devices.md)デバイスのイジェクト ボタンをクリックします。 フレームワークでは、ドライバーがあるない限り、デバイスを削除または無効にするができます。

-   呼ばれる[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)特別なファイルは、デバイスで開いているとします。

-   呼ばれる[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)します。

-   指定された、 [ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)コールバック関数、およびコールバック関数を削除が拒否しました。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最上位である driver 以降では、シーケンスで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)コールバック関数。

2.  フレームワークは、すべてのドライバーの電源管理対象の I/O キューを停止します。

3.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)、 [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)、および[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)コールバックが作成された DMA チャネルごと (存在する) 場合に機能します。

4.  フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856) (存在する) 場合は、コールバック関数を呼び出してドライバーのおよび[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック関数 (存在する) 場合各割り込みのドライバーは、デバイスの割り込みを無効にできます。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855) (存在する) 場合、コールバック関数。

6.  フレームワークは、ドライバーの[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)コールバック関数。

8.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)コールバック関数。

バス ドライバーは、最後に呼び出されるスタックのドライバーです。 ときに、フレームワークが、バス ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855) D3 にコールバック関数では、コールバック関数の設定 (バスの子デバイス) のデバイスの電源の状態。 フレームワークを呼び出すときに、バス ドライバーを制御できますその[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数を呼び出して[  **。WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)します。

### <a href="" id="surprise-removal"></a> 突然の取り外し

ユーザーはデバイスが予期せず切り離されます。 デバイスのバスのバス ドライバーは、デバイスがないと、呼び出しを検出します。 [ **WdfChildListUpdateChildDescriptionAsMissing**](https://msdn.microsoft.com/library/windows/hardware/ff545674)します。

各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最上位である driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913) (存在する) 場合、コールバック関数。

2.  それが接続されていない作業 (D0) の状態で、デバイスがでしたが、すべてのドライバーの I/O キューの電源管理対象のフレームワークを停止します。

3.  デバイスの作業 (D0) が状態だった場合、接続できなかったし、場合、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)コールバック関数。

4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)、 [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)、および[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)コールバックが作成された DMA チャネルごと (存在する) 場合に機能します。

5.  フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)と[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック関数 (存在する場合)、ドライバーがデバイスの割り込みを無効にするようにします。

6.  フレームワークは、ドライバーの[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855) (存在する) 場合、コールバック関数。

7.  フレームワークは、ドライバーの[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

8.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)コールバック関数。

9.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)コールバック関数。

デバイスをいつでもが予期せず削除できることに注意してください。 そのため、フレームワークは、ドライバーを呼び出すことができます[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)前の手順で示す以外の時にコールバック関数。 たとえば、ユーザーの中にデバイスが予期せずコールバックある[低電力状態に入って](a-device-enters-a-low-power-state.md)、フレームワークが呼び出すことができます、 [ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)コールバック関数の呼び出し後、 [ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数。 コーディングする必要があります、 [ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)およびその他のコールバック関数が特定の順序でと呼ばれることを前提としている方法でコールバック関数。

さらに、フレームワークには、デバイスの同期されません[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)そのデバイスの前の手順で、コールバック関数のいずれかでコールバック関数が一覧表示します。 そのため、 [ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)コールバック関数は、上記のコールバック関数のもう 1 つも実行中に実行可能性があります。

 

 





