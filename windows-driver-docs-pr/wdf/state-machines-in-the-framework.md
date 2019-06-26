---
title: フレームワークでのステート マシン
description: フレームワークでのステート マシン
ms.assetid: 5ef307c6-0310-4a83-a63f-3a6d96782013
keywords:
- PnP WDK KMDF、ステート マシン
- プラグ アンド プレイ WDK KMDF、ステート マシン
- 電源管理 WDK KMDF、ステート マシン
- WDK KMDF のマシンを状態します。
- WDK KMDF を状態します。
- PnP 状態マシン WDK KMDF
- 電源状態が WDK KMDF
- ステート マシンの現在状態 WDK KMDF
- WDK KMDF、ステート マシンの状態情報
- 電源ポリシー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca35d5f5137392ec3937ebef6ce251e21ea68d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376178"
---
# <a name="state-machines-in-the-framework"></a>フレームワークでのステート マシン


各デバイスの状態を追跡するのには、フレームワークは、PnP ステート マシン、電源のステート マシン、および電源ポリシーのステート マシンを使用します。 フレームワークは、システムに接続されている各デバイスの場合は、各ステート マシンのインスタンスを作成します。

>[!NOTE]
>この機能は、Microsoft 内部使用のみです。

ドライバーはこの情報を理解する必要がある場合は、フレームワークは、2 つのインターフェイスのセットを提供します。

-   ドライバーによって提供されるイベントのコールバック関数のセット。

    ドライバーは、ステート マシンのいずれかを入力または特定の状態を終了するたびに、次のコールバックのいずれかのフレームワーク呼び出しが機能を要求できます。

    -   [*EvtDevicePnpStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)します。
    -   [*EvtDevicePowerStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)します。
    -   [*EvtDevicePowerPolicyStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)します。
-   ステート マシンの現在の状態を返すメソッドのセット。

    ドライバーは、特定のデバイス用のステート マシンのいずれかの現在の状態を確認するのには、次のメソッドのいずれかを呼び出すことができます。

    -   [**WdfDeviceGetDevicePnpState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepnpstate)
    -   [**WdfDeviceGetDevicePowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerstate)
    -   [**WdfDeviceGetDevicePowerPolicyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerpolicystate)

 

 





