---
title: バッテリ Miniclass ドライバーの DriverEntry ルーチン
description: バッテリ Miniclass ドライバーの DriverEntry ルーチン
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DriverEntry WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c69b4003285662ab64f95ab3566e3f4dbeb5ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560213"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>バッテリ Miniclass ドライバーの DriverEntry ルーチン


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを miniclass ドライバーを初期化します。

Miniclass ドライバーの[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、次のドライバー固有のエントリ ポイントを設定します。

-   [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)で日常的な*DriverObject*-&gt;**DriverUnload**

-   ドライバーの[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)で日常的な*DriverObject*-&gt;**DriverExtension** - &gt; **AddDevice**

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff550784)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_を作成します。**](https://msdn.microsoft.com/library/windows/hardware/ff550729)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/ff550720)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)のコールバック関数で*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)\]します。

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

PnP マネージャー呼び出す miniclass ドライバーのまでバッテリ固有の状態情報が不明なので*AddDevice* 、ルーチン、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンはありませんこのような任意の状態を初期化します。 デバイス固有の初期化が実行される、 *AddDevice*ルーチン。

ルーチン固有の追加要件は、次のトピックを参照してください。

[バッテリ Miniclass ドライバーの AddDevice ルーチン](adddevice-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchDeviceControl ルーチン](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchSystemControl ルーチン](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーをアンロード ルーチン](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




