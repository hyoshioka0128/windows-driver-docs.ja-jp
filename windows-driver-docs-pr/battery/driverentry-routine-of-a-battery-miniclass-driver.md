---
title: バッテリ ミニクラス ドライバーの DriverEntry ルーチン
description: バッテリ ミニクラス ドライバーの DriverEntry ルーチン
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DriverEntry WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eda92cce32bb1e82e65d7b26a91ce297a690703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832219"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DriverEntry ルーチン


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、miniclass ドライバーを初期化します。

Miniclass ドライバーの[*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、次のドライバー固有のエントリポイントを設定します。

-   *Driverobject*の[*unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン-&gt;**driverobject**

-   *Driverobject*のドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン-&gt;**driverobject**-&gt;**AddDevice**

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)\]

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)\]

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)\]

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)\]

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)\]

-   *Driverobject*の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) Callback 関数-&gt;**MajorFunction**\[[**IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)\]です。

次のサンプルコードは、架空の NewBatt miniclass ドライバーのエントリポイントを初期化します。

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

バッテリ固有の状態情報は、PnP マネージャーが miniclass ドライバーの*AddDevice*ルーチンを呼び出すまで不明であるため、 [*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、このような状態を初期化しません。 デバイス固有の初期化は、 *AddDevice*ルーチンで実行されます。

その他のルーチン固有の要件については、次のトピックを参照してください。

[AddDevice のバッテリ Miniclass ドライバーのルーチン](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl のバッテリ Miniclass ドライバーのルーチン](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl のバッテリ Miniclass ドライバーのルーチン](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーのアンロードルーチン](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




