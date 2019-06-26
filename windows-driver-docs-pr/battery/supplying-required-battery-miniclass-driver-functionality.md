---
title: 必要なバッテリ ミニクラス ドライバー機能の提供
description: 必要なバッテリ ミニクラス ドライバー機能の提供
ms.assetid: d33d3c8c-f867-40dc-901c-6b0dd5d57dac
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- ルーチンの WDK バッテリ
- バッテリ miniclass ドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e42ab0d8d273fd18246bdc84432b3366f3ef888b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364724"
---
# <a name="supplying-required-battery-miniclass-driver-functionality"></a>必要なバッテリ ミニクラス ドライバー機能の提供


## <span id="ddk_supplying_required_battery_miniclass_driver_functionality_dg"></span><span id="DDK_SUPPLYING_REQUIRED_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


サポートに必要なルーチンに加え[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)バッテリの miniclass ドライバーは、次のルーチンをいる必要があります。

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

[アンロード](unload-routine-of-a-battery-miniclass-driver.md)

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)、[アンロード](unload-routine-of-a-battery-miniclass-driver.md)、 [DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)、および[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)は標準のドライバー ルーチン。 DriverEntry 名が必要です、ため、オペレーティング システムを使用すると、ドライバーの開始時に呼び出すことができます。 適切なデータ構造のアドレスが正しく読み込まれている限り、各自の判断でその他のドライバーのルーチンの名前を選択できます。

[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)ルーチンが miniclass ドライバーによって提供され、バッテリのクラス ドライバーによって呼び出されます。 Miniclass ドライバーを記述する場合は、これらのルーチンのいずれかの機能を実装するには、しないこともできます。ただし、ルーチンのエントリ ポイントを指定する必要がありますそれにもかかわらず、およびルーチンは、状態を返す必要があります\_いない\_サポートされています。 これらのルーチンのプロトタイプは Batclass.h に表示されます。

バッテリ miniclass ドライバーでは、次のヘッダー ファイルを含める必要があります。

-   Batclass.h

-   Ntddk.h または Wdm.h

 

 




