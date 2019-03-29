---
title: 非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用
description: 非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用
ms.assetid: b4b6add2-0e27-4af7-b6bf-5e47db7db560
keywords:
- 非 PnP ドライバー WDK KMDF
- カーネル モード ドライバー WDK KMDF、PnP
- KMDF WDK、PnP
- カーネル モード ドライバー フレームワーク WDK、PnP
- プラグ アンド プレイ WDK KMDF、非 PnP ドライバー
- PnP WDK KMDF、非 PnP ドライバー
- フレームワーク ベースのドライバー WDK KMDF、PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e7efa27b548eb26917092f6463d1f63470fb2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573581"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用





プラグ アンド プレイ (PnP) をサポートしていないデバイスのドライバーを作成する場合、ドライバーが必要です。

-   設定、 [ **WdfDriverInitNonPnpDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)フラグ、 [ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)構造体の**DriverInitFlags**メンバー。

-   提供、 [ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)イベント コールバック関数。

-   Framework デバイス オブジェクトを作成するには、のみを表す[デバイス オブジェクトを制御](using-control-device-objects.md)します。

ドライバーには、デバイスをサポートしていない PnP 場合*いない*提供、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 代わりに、ドライバーは、そのデバイスが存在するかどうかを決定する必要があります。

 

 





