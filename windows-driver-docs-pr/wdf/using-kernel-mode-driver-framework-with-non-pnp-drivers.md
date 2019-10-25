---
title: 非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用
description: 非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用
ms.assetid: b4b6add2-0e27-4af7-b6bf-5e47db7db560
keywords:
- 非 PnP ドライバー WDK KMDF
- カーネルモードドライバー WDK KMDF、PnP
- KMDF WDK、PnP
- カーネルモードドライバーフレームワーク WDK、PnP
- プラグアンドプレイ WDK KMDF、PnP 以外のドライバー
- PnP WDK KMDF、PnP 以外のドライバー
- フレームワークベースのドライバー WDK KMDF、PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7afb5e0cfb200905de55cdd41271e61e9ec1298b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845435"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>非 PnP ドライバーでのカーネルモード ドライバー フレームワークの使用





プラグアンドプレイ (PnP) をサポートしていないデバイス用のドライバーを作成する場合、ドライバーは次のことを行う必要があります。

-   [**WDF\_DRIVER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体の**driverinitflags**メンバーに[**WdfDriverInitNonPnpDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグを設定します。

-   [*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)イベントコールバック関数を指定します。

-   [コントロールデバイスオブジェクト](using-control-device-objects.md)のみを表すフレームワークデバイスオブジェクトを作成します。

デバイスで PnP がサポートされていない場合、ドライバーは[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を提供し*ません*。 代わりに、ドライバーはデバイスが存在するかどうかを判断する必要があります。

 

 





