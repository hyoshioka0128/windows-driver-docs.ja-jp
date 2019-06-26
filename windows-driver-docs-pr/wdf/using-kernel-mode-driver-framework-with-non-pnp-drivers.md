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
ms.openlocfilehash: e462053b368f6c8de9abd407cd477d22e5ef1643
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372244"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用





プラグ アンド プレイ (PnP) をサポートしていないデバイスのドライバーを作成する場合、ドライバーが必要です。

-   設定、 [ **WdfDriverInitNonPnpDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグ、 [ **WDF\_ドライバー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体の**DriverInitFlags**メンバー。

-   提供、 [ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)イベント コールバック関数。

-   Framework デバイス オブジェクトを作成するには、のみを表す[デバイス オブジェクトを制御](using-control-device-objects.md)します。

ドライバーには、デバイスをサポートしていない PnP 場合*いない*提供、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 代わりに、ドライバーは、そのデバイスが存在するかどうかを決定する必要があります。

 

 





