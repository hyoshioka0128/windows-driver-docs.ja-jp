---
title: 機能ドライバーでの PnP と電源管理のサポート
description: 機能ドライバーでの PnP と電源管理のサポート
ms.assetid: 487d4a69-a8a8-406c-8572-688388deabe3
keywords:
- PnP WDK KMDF, 関数ドライバー
- プラグアンドプレイ WDK KMDF, 関数ドライバー
- 電源管理 WDK KMDF, 関数ドライバー
- 関数ドライバー WDK KMDF
- 電源ポリシー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 518e7a104d572e3fa4d9c63e3f1db28edb85ca7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831716"
---
# <a name="supporting-pnp-and-power-management-in-function-drivers"></a>機能ドライバーでの PnP と電源管理のサポート


*関数ドライバー*はデバイスの動作を制御するため、デバイスのハードウェアにアクセスします。 これらのドライバーは、PnP および電源管理操作をサポートし、通常、[デバイスオブジェクトを作成](creating-a-framework-device-object.md)するときに複数のイベントコールバック関数を登録する必要があります。

通常、関数ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数は、 [**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)を呼び出して、次のコールバック関数を登録します。

-   デバイスのシステムによって割り当てられたリソースをドライバーに配信する、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)。 ドライバーは、デバイスのバス相対メモリをプロセッサの仮想アドレス空間にマップするなどの操作を実行できます。これにより、ドライバーがハードウェアにアクセスできるようになります。

-   [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)は、ドライバーのデバイスが動作 (D0) 状態になるたびに必要な、ファームウェアの読み込みなどの操作を実行します。

-   [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)。ドライバーのデバイスが動作中 (D0) 状態になり、省電力状態になるたびに必要な操作を実行します。

-   [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)は、[*ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)が割り当てられているシステムリソースを解放します。

すべてのフレームワーク定義のコールバック関数と同様に、上記の一覧にあるものは任意です。 ドライバーが必要な場合にのみ指定する必要があります。

関数ドライバーは、 [**WdfDeviceSetPnpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities)および[**Wdfdevicesetpowercapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities)を呼び出して、デバイスの PnP および電源管理機能をオペレーティングシステムに報告できます。

通常は、ほとんどの i/o 要求に対して、フレームワークの*電源管理 i/o キュー*を使用します。 I/o キューが電源管理されている場合、フレームワークは、デバイスが動作 (D0) 状態にある場合にのみ、ドライバーに要求を配信します。 電源管理の i/o キューの詳細については、「 [I/o キューの電源管理](power-management-for-i-o-queues.md)」を参照してください。

通常、デバイスの関数ドライバーは、ドライバースタックの*電源ポリシーの所有者*です。 電源ポリシーの所有者は、デバイスの適切な[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)を判断し、デバイスの電源状態が変更されるたびにデバイスのドライバースタックに要求を送信します。 フレームワークベースのドライバーの場合、フレームワークはこの役割を処理するので、デバイスの電源状態の変更を要求するためのコードをドライバーに提供する必要はありません。

電源ポリシーの所有者には、次の2つの追加の責任があります。アイドル状態になったときに低電力状態になるデバイスの能力を制御し、システムが[動作中 (S0) 状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)のままになっている場合、デバイスがスリープ状態になったときにスリープ信号を生成する機能を制御します。外部イベントを低電力状態から検出します。 デバイスにアイドルまたはウェイクアップ機能がある場合、関数ドライバーは追加のコールバック関数を提供できます。 電源ポリシー所有者の役割の詳細については、「[電源ポリシーの所有権](power-policy-ownership.md)」を参照してください。

 

 





