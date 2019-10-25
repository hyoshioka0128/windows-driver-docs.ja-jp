---
title: フレームワークでのステート マシン
description: フレームワークでのステート マシン
ms.assetid: 5ef307c6-0310-4a83-a63f-3a6d96782013
keywords:
- PnP WDK KMDF、ステートマシン
- WDK KMDF、ステートマシンプラグアンドプレイ
- 電源管理 WDK KMDF、ステートマシン
- ステートマシン WDK KMDF
- 状態 WDK KMDF
- PnP ステートマシン WDK KMDF
- 電源状態 WDK KMDF
- 現在のステートマシンの状態 WDK KMDF
- 状態情報 WDK KMDF、ステートマシン
- 電源ポリシー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff5a547158396409186ede25d11df3a073ab58c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845196"
---
# <a name="state-machines-in-the-framework"></a>フレームワークでのステート マシン


各デバイスの状態を追跡するために、フレームワークは PnP ステートマシン、電源状態のマシン、および電源ポリシーのステートマシンを使用します。 フレームワークは、システムに接続されている各デバイスについて、各ステートマシンのインスタンスを作成します。

>[!NOTE]
>この機能は、Microsoft の内部でのみ使用されます。

この情報を知る必要があるドライバーの場合、フレームワークには次の2つのインターフェイスセットが用意されています。

-   ドライバーが提供するイベントコールバック関数のセット。

    ドライバーは、いずれかのステートマシンが特定の状態に入ったり、終了したときに、次のいずれかのコールバック関数を呼び出すようにフレームワークに要求できます。

    -   [*EvtDevicePnpStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)。ドライバーは[**WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)を呼び出すことによって登録します。
    -   [*EvtDevicePowerStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)。ドライバーは[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)を呼び出すことによって登録します。
    -   [*EvtDevicePowerPolicyStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification)。ドライバーは[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)を呼び出すことによって登録します。
-   ステートマシンの現在の状態を返すメソッドのセット。

    ドライバーは、次のいずれかのメソッドを呼び出して、特定のデバイスのいずれかのステートマシンの現在の状態を確認できます。

    -   [**WdfDeviceGetDevicePnpState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepnpstate)
    -   [**WdfDeviceGetDevicePowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerstate)
    -   [**WdfDeviceGetDevicePowerPolicyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerpolicystate)

 

 





