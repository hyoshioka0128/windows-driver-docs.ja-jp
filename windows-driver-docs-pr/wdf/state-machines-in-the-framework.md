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
ms.openlocfilehash: ce09ece00bf70351ab95a528bb236209cc96849d
ms.sourcegitcommit: 39c0b7e84e5087447493507a478b870c7a834446
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2019
ms.locfileid: "66458844"
---
# <a name="state-machines-in-the-framework"></a>フレームワークでのステート マシン


各デバイスの状態を追跡するのには、フレームワークは、PnP ステート マシン、電源のステート マシン、および電源ポリシーのステート マシンを使用します。 フレームワークは、システムに接続されている各デバイスの場合は、各ステート マシンのインスタンスを作成します。

>[!NOTE]
>この機能は、Microsoft 内部使用のみです。

ドライバーはこの情報を理解する必要がある場合は、フレームワークは、2 つのインターフェイスのセットを提供します。

-   ドライバーによって提供されるイベントのコールバック関数のセット。

    ドライバーは、ステート マシンのいずれかを入力または特定の状態を終了するたびに、次のコールバックのいずれかのフレームワーク呼び出しが機能を要求できます。

    -   [*EvtDevicePnpStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540874)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546057)します。
    -   [*EvtDevicePowerStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540878)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071)します。
    -   [*EvtDevicePowerPolicyStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540876)、呼び出すことによって、ドライバーを登録する[ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)します。
-   ステート マシンの現在の状態を返すメソッドのセット。

    ドライバーは、特定のデバイス用のステート マシンのいずれかの現在の状態を確認するのには、次のメソッドのいずれかを呼び出すことができます。

    -   [**WdfDeviceGetDevicePnpState**](https://msdn.microsoft.com/library/windows/hardware/ff545969)
    -   [**WdfDeviceGetDevicePowerState**](https://msdn.microsoft.com/library/windows/hardware/ff545985)
    -   [**WdfDeviceGetDevicePowerPolicyState**](https://msdn.microsoft.com/library/windows/hardware/ff545974)

 

 





