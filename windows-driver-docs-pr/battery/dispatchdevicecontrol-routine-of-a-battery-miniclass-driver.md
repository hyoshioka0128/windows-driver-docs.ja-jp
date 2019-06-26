---
title: バッテリ ミニクラス ドライバーの DispatchDeviceControl ルーチン
description: バッテリ ミニクラス ドライバーの DispatchDeviceControl ルーチン
ms.assetid: 26313dcc-9f37-4c5e-a21e-c4d8a50ff564
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DispatchDeviceControl ルーチン
- Ioctl WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8722a72068dc2af185e70a2db6b468cf1dfdc3dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354075"
---
# <a name="dispatchdevicecontrol-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DispatchDeviceControl ルーチン


## <span id="ddk_dispatchdevicecontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHDEVICECONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


電源マネージャーがデバイスの制御 Irp を送信します (IRP\_MJ\_デバイス\_コントロール) を複合バッテリ ドライバーを通じて miniclass ドライバーにします。 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)バッテリ miniclass ドライバーのルーチンは、バッテリ Ioctl にはが含まれている Irp を処理します。

[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、miniclass ドライバーは、クラス ドライバーを呼び出すことができます[ **BatteryClassIoctl** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ルーチンを実行するにはシステム定義のデバイス管理タスク。**BatteryClassIoctl**バッテリのデバイスの制御の Ioctl を処理します。

[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、次を行う必要があります。

1.  Miniclass ドライバーには、任意のプライベート Ioctl が定義されている場合は、現在の IOCTL がそれらの間がかどうかを決定します。 そうである場合、要求された操作の実行、IO を指定する、IRP の完了\_なし\_手順 4 に増分値、および移動します。

2.  IOCTL が miniclass ドライバーで定義されたプライベート IOCTL でない場合は、呼び出す**BatteryClassIoctl**、IRP とによって返されるクラスのハンドルを渡す[ **BatteryClassInitializeDevice** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice). 例:

    ```cpp
    Status = BatteryClassIoctl (NewBattNP->ClassHandle, Irp);
    ```

    クラス ドライバーの[ **BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ルーチンは、指定されたバッテリの IOCTL が対象として かどうかを決定します。 場合は、対応するために、呼び出し[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)ルーチンを要求を満たすために、状態を返す、IRP が完了して\_成功します。 それ以外の場合、ステータスを返す\_いない\_サポートされています。

3.  場合[ **BatteryClassIoctl** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ステータスを返します\_いない\_下ドライバーに IRP を渡すバッテリの IRP ではないことを示す、サポートされています。

4.  独自の関数の戻り値として返される状態を渡します。

 

 




