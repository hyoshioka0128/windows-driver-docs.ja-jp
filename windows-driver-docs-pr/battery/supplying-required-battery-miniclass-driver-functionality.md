---
title: 必要なバッテリ ミニクラス ドライバー機能の提供
description: 必要なバッテリ ミニクラス ドライバー機能の提供
ms.assetid: d33d3c8c-f867-40dc-901c-6b0dd5d57dac
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- ルーチン WDK バッテリ
- バッテリ miniclass ドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfb9b8412006ea94828fc5a034a805eeeaf258a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832218"
---
# <a name="supplying-required-battery-miniclass-driver-functionality"></a>必要なバッテリ ミニクラス ドライバー機能の提供


## <span id="ddk_supplying_required_battery_miniclass_driver_functionality_dg"></span><span id="DDK_SUPPLYING_REQUIRED_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)をサポートするために必要なルーチンに加えて、バッテリ miniclass ドライバーには次のルーチンが必要です。

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)

[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[*BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryStatus*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)

[*BatteryMiniQueryInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniSetInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_information_callback)

[*BatteryMiniSetStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)

[*BatteryMiniDisableStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)

[取り除き](unload-routine-of-a-battery-miniclass-driver.md)

[Driverentry](driverentry-routine-of-a-battery-miniclass-driver.md)、 [Unload](unload-routine-of-a-battery-miniclass-driver.md)、 [DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)、および[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)は、標準ドライバールーチンです。 ドライバーの開始時にオペレーティングシステムが呼び出しを行うことができるように、名前 DriverEntry が必要です。 適切なデータ構造に適切に読み込まれていれば、他のドライバールーチンの名前を自由に選択できます。

[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)ルーチンは、miniclass ドライバーによって提供され、バッテリクラスドライバーによって呼び出されます。 Miniclass ドライバーを作成する場合は、これらのルーチンの機能を実装しないことを選択できます。ただし、ルーチンのエントリポイントを指定する必要があります。ルーチンは、サポートされて\_いない状態\_返す必要があります。 これらのルーチンのプロトタイプは、Batclass に表示されます。

バッテリ miniclass ドライバーには、次のヘッダーファイルが含まれている必要があります。

-   Batclass

-   Ntddk または Wdm

 

 




