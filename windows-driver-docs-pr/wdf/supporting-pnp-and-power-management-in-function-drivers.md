---
title: 機能ドライバーでの PnP と電源管理のサポート
description: 機能ドライバーでの PnP と電源管理のサポート
ms.assetid: 487d4a69-a8a8-406c-8572-688388deabe3
keywords:
- PnP WDK KMDF、関数のドライバー
- プラグ アンド プレイ WDK KMDF、関数のドライバー
- 電源管理 WDK KMDF、関数のドライバー
- 機能ドライバー WDK KMDF
- 電源ポリシー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e41bb55e0bbc5460dc6653d8cab5bf45139906c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368058"
---
# <a name="supporting-pnp-and-power-management-in-function-drivers"></a>機能ドライバーでの PnP と電源管理のサポート


*関数のドライバー*デバイスの操作を制御し、デバイスのハードウェアにアクセスするためです。 これらのドライバーの PnP や電源管理操作をサポートして、通常いくつかのイベントのコールバック関数を登録する必要があるときに、[デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。

通常、関数ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベント コールバック関数の呼び出し[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)次のコールバック関数を登録します。

-   [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)ドライバーにデバイスのシステムによって割り当てられたリソースを提供します。 ドライバーは、ハードウェアをドライバーにアクセスできるように、プロセッサの仮想アドレス空間に、デバイスのバスの相対メモリのマッピングなどの操作を実行できます。

-   [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)ドライバーのデバイスがその作業 (D0) 状態になるなど、読み込み、ファームウェアであるために必要なするごとに、操作を実行します。

-   [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)ドライバーのデバイスがの作業 (D0) 状態のままし、低電力状態に入るたびに必要な操作を実行します。

-   [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)、システム リソースを解放するを[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)割り当てられます。

すべてのフレームワークで定義されたコールバック関数と同様に、上記の一覧で使用されているは省略可能です。 ドライバーでは、その必要がある場合にのみ、それらを指定するがあります。

ドライバーの関数を呼び出すことができます[ **WdfDeviceSetPnpCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities)と[ **WdfDeviceSetPowerCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities)デバイスの PnP を報告してオペレーティング システムに電源管理機能。

通常、フレームワークを使用する*電源管理対象の I/O キュー*ほとんどの I/O 要求。 I/O キューが電源管理対象の場合、フレームワークは、デバイスの作業 (D0) 状態にある場合にのみ、ドライバーに要求を配信します。 電源管理対象の I/O キューの詳細については、次を参照してください。[の I/O キューの電源管理](power-management-for-i-o-queues.md)します。

通常、デバイスの機能のドライバーは、*電源ポリシー所有者*ドライバー スタックの。 電源ポリシー所有者は、適切な決定[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)デバイスの電源の状態が変更されるたびに、デバイスのドライバー スタックへのデバイスと送信要求。 Framework ベースのドライバーでは、フレームワークは、ドライバーのデバイスの電源状態の変更を要求するコードを指定する必要はありませんので、責任を処理します。

電源ポリシーの所有者が 2 つの責任を負う: がアイドル状態と、システムのままにする場合は、低電力状態を入力するデバイスの機能を制御、 [(S0) の状態を操作](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)、生成するデバイスの機能を制御し、低電力状態から外部イベントを検出した場合に、信号をスリープ解除します。 場合は、デバイスがアイドル状態または機能をスリープ解除、関数には、ドライバーは追加のコールバック関数を提供できます。 電源ポリシーの所有者の役割の詳細については、次を参照してください。[電源ポリシー所有権](power-policy-ownership.md)します。

 

 





