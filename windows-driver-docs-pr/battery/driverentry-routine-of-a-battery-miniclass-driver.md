---
title: バッテリ ミニクラス ドライバーの DriverEntry ルーチン
description: バッテリ ミニクラス ドライバーの DriverEntry ルーチン
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DriverEntry WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7b25b1095d4e684239912c8e08137f68163d7e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354069"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DriverEntry ルーチン


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを miniclass ドライバーを初期化します。

Miniclass ドライバーの[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンは、次のドライバー固有のエントリ ポイントを設定します。

-   [*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)で日常的な*DriverObject*-&gt;**DriverUnload**

-   ドライバーの[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)で日常的な*DriverObject*-&gt;**DriverExtension** - &gt; **AddDevice**

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_を作成します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)\]します。

次のサンプル コードでは、架空の NewBatt miniclass ドライバーに対してこれらのエントリ ポイントを初期化します。

```cpp
DriverObject->DriverUnload = NewBattUnload;
DriverObject->DriverExtension->AddDevice = NewBattAddDevice; 
DriverObject->MajorFunction[IRP_MJ_DEVICE_CONTROL] = NewBattDispatchDeviceControl;
DriverObject->MajorFunction[IRP_MJ_CREATE] = NewBattDispatchCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = NewBattDispatchClose;
DriverObject->MajorFunction[IRP_MJ_PNP] = NewBattDispatchPnp;
DriverObject->MajorFunction[IRP_MJ_POWER] = NewBattDispatchPower;
DriverObject->MajorFunction[IRP_MJ_SYSTEM_CONTROL] = NewBattSystemControl;
```

PnP マネージャー呼び出す miniclass ドライバーのまでバッテリ固有の状態情報が不明なので*AddDevice* 、ルーチン、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンはありませんこのような任意の状態を初期化します。 デバイス固有の初期化が実行される、 *AddDevice*ルーチン。

ルーチン固有の追加要件は、次のトピックを参照してください。

[バッテリ Miniclass ドライバーの AddDevice ルーチン](adddevice-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchDeviceControl ルーチン](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchSystemControl ルーチン](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーをアンロード ルーチン](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




