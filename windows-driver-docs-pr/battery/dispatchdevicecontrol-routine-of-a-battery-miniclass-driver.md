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
ms.openlocfilehash: eadc5473065b43e4a736c8bcfcbda8a7231a07cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832226"
---
# <a name="dispatchdevicecontrol-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DispatchDeviceControl ルーチン


## <span id="ddk_dispatchdevicecontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHDEVICECONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


電源マネージャーは、デバイス制御 Irp (IRP\_MJ\_デバイス\_コントロール) を、複合バッテリドライバーを介して miniclass ドライバーに送信します。 バッテリの miniclass ドライバーの[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、バッテリ ioctl を含む irp を処理します。

[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)では、miniclass ドライバーはクラスドライバーの[**BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ルーチンを呼び出して、システム定義のデバイス制御タスクを実行できます。**BatteryClassIoctl**は、バッテリのデバイス制御の ioctl を処理します。

[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでは、次の操作を行う必要があります。

1.  Miniclass ドライバーがプライベート Ioctl を定義する場合は、現在の IOCTL がその中にあるかどうかを判断します。 その場合は、要求された操作を実行し、IRP を完了し、IO\_\_の増分値を指定して、手順4に進みます。

2.  IOCTL が miniclass ドライバーによって定義されるプライベート IOCTL でない場合は、 **BatteryClassIoctl**を呼び出して、 [**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)によって返される IRP およびクラスハンドルを渡します。 次に、例を示します。

    ```cpp
    Status = BatteryClassIoctl (NewBattNP->ClassHandle, Irp);
    ```

    クラスドライバーの[**BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ルーチンは、IOCTL が指定されたバッテリを対象としているかどうかを判断します。 その場合は、対応する[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)ルーチンを呼び出して要求を満たし、IRP を完了し、状態\_SUCCESS に戻ります。 それ以外の場合、サポートされていない状態\_返さ\_ます。

3.  [**BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)が\_サポートされていない状態\_返される場合は、これがバッテリの irp でないことを示します。 irp を次の下位のドライバーに渡します。

4.  返された状態を独自の関数の戻り値として渡します。

 

 




