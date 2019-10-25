---
title: バッテリ ミニクラス ドライバーの FDO の作成
description: バッテリ ミニクラス ドライバーの FDO の作成
ms.assetid: 3178710b-8e4a-4f9c-893b-1d06c4a3f7ff
keywords:
- バッテリ miniclass ドライバー WDK、FDOs
- FDOs WDK バッテリ
- 機能デバイスオブジェクト WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 331d8b1f5735611f2c6d0663d260a14e2d8f116d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829913"
---
# <a name="creating-an-fdo-in-the-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの FDO の作成


## <span id="ddk_creating_an_fdo_in_the_battery_miniclass_driver_dg"></span><span id="DDK_CREATING_AN_FDO_IN_THE_BATTERY_MINICLASS_DRIVER_DG"></span>


Miniclass ドライバーは、次のように FDO を作成し、デバイスのデバイススタックにアタッチする必要があります。

1.  [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出して、現在のデバイスの FDO を次のように作成します。

    ```cpp
    Status = IoCreateDevice(
             DriverObject,
             sizeof (DeviceExtension),
             NULL,
             FILE_DEVICE_BATTERY,
             0,
             FALSE,
             &Fdo
             );
    ```

    [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)への入力パラメーターは、 *AddDevice*ルーチンに渡されたドライバーオブジェクトへのポインター、デバイス拡張機能のサイズ、デバイス名の代わりの NULL、およびシステム定義デバイスの種類 (ファイル\_デバイス\_バッテリ)。 バッテリ miniclass ドライバーでは、 *DeviceCharacteristics*パラメーターに0を指定できます。このパラメーターは、これらのドライバーには関係ありません。 複数のスレッドがバッテリに i/o 要求を送信できるため、miniclass ドライバーは、*排他*パラメーターとして FALSE を渡します。 **IoCreateDevice**は、作成された FDO へのポインターを返します。

2.  返された FDO で、フラグとスタックサイズを設定します。 次に、例を示します。

    ```cpp
    Fdo->Flags |= DO_BUFFERED_IO;
    Fdo->Flags |= DO_POWER_PAGABLE;
    Fdo->StackSize = Pdo->StackSize + 2;
    ```

    DO\_バッファリング\_IO フラグを設定すると、miniclass ドライバーは Irp にバッファー i/o を使用できます。 DO\_POWER\_PAGABLE フラグを設定すると、ドライバーがページング可能であり、IRQL &gt;= ディスパッチ\_レベルで電源 Irp を取得できなくなります。 最後に、バッテリの Irp には追加のスタック位置が必要であるため、ドライバーが IRP を PDO に渡すことができるように、miniclass ドライバーは**StackSize**を pdo スタックサイズに加えて2に設定する必要があります。

3.  デバイスの PDO へのポインター、FDO へのポインター、デバイスの種類、デバイスの名前、デバイスの拡張機能に必要なその他の状態を格納します。 次に、例を示します。

    ```cpp
    NewBatt = (PNEW_BATT) Fdo->DeviceExtension;
    NewBatt->Type = NEW_BATTERY_TYPE;
    NewBatt->Fdo = Fdo;
    NewBatt->Pdo = Pdo;
    NewBatt->IsCacheValid = FALSE;
    ```

    この例では、デバイス拡張機能に FDO と PDO へのポインターを格納します。 (PnP マネージャーは、 *AddDevice*への*PhysicalDeviceObject*ポインター入力として PDO へのポインターを提供しました)。さらに、上記の例では、独自のバッテリの種類 (新しい\_バッテリ\_の種類、この架空の miniclass ドライバーの他の場所で定義されています)、およびキャッシュされた情報が有効かどうかを追跡します。

    デバイス拡張機能に格納されている情報を確認します。 たとえば、スマートバッテリドライバーでは、バッテリの数、バッテリセレクターが存在するかどうかを示すブール値、および必要に応じてそのバッテリセレクターに関する情報を保持することができます。

4.  [**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出して、FDO をデバイススタックにアタッチし、返されたポインターを次のように格納します。

    ```cpp
    NewBatt->LowerDO = IoAttachDeviceToDeviceStack(Fdo,Pdo);
    ```

    この呼び出しは、デバイス拡張機能に格納されている次の下位デバイスオブジェクトへのポインターを返します。

5.  次の手順に従って、FDO の [\_デバイス\_初期化] フラグをオフにします。

    ```cpp
    Fdo->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

    DO\_DEVICE\_初期化フラグをオフにすると、デバイスオブジェクトをデバイススタックの上位のコンポーネントから開くことができます。

 

 




