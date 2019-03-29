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
ms.openlocfilehash: 4b6e2464a483e233cc195e2c79887d1fbf5521b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571545"
---
# <a name="supplying-required-battery-miniclass-driver-functionality"></a>必要なバッテリ ミニクラス ドライバー機能の提供


## <span id="ddk_supplying_required_battery_miniclass_driver_functionality_dg"></span><span id="DDK_SUPPLYING_REQUIRED_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


サポートに必要なルーチンに加え[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)バッテリの miniclass ドライバーは、次のルーチンをいる必要があります。

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)

[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[*BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)

[*BatteryMiniQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff536274)

[*BatteryMiniQueryInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536273)

[*BatteryMiniSetInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536276)

[*BatteryMiniSetStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536277)

[*BatteryMiniDisableStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536272)

[アンロード](unload-routine-of-a-battery-miniclass-driver.md)

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)、[アンロード](unload-routine-of-a-battery-miniclass-driver.md)、 [DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)、および[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)は標準のドライバー ルーチン。 DriverEntry 名が必要です、ため、オペレーティング システムを使用すると、ドライバーの開始時に呼び出すことができます。 適切なデータ構造のアドレスが正しく読み込まれている限り、各自の判断でその他のドライバーのルーチンの名前を選択できます。

[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)ルーチンが miniclass ドライバーによって提供され、バッテリのクラス ドライバーによって呼び出されます。 Miniclass ドライバーを記述する場合は、これらのルーチンのいずれかの機能を実装するには、しないこともできます。ただし、ルーチンのエントリ ポイントを指定する必要がありますそれにもかかわらず、およびルーチンは、状態を返す必要があります\_いない\_サポートされています。 これらのルーチンのプロトタイプは Batclass.h に表示されます。

バッテリ miniclass ドライバーでは、次のヘッダー ファイルを含める必要があります。

-   Batclass.h

-   Ntddk.h または Wdm.h

 

 




