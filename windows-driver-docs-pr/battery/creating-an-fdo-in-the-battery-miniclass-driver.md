---
title: バッテリ ミニクラス ドライバーの FDO の作成
description: バッテリ ミニクラス ドライバーの FDO の作成
ms.assetid: 3178710b-8e4a-4f9c-893b-1d06c4a3f7ff
keywords:
- バッテリ miniclass ドライバー WDK、Fdo
- Fdo WDK バッテリ
- 機能のデバイス オブジェクトの WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88fdf96a5adcf0cb1bbf60421c63e715c1960e75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571551"
---
# <a name="creating-an-fdo-in-the-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの FDO の作成


## <span id="ddk_creating_an_fdo_in_the_battery_miniclass_driver_dg"></span><span id="DDK_CREATING_AN_FDO_IN_THE_BATTERY_MINICLASS_DRIVER_DG"></span>


Miniclass ドライバーは、FDO を作成し、次のように、デバイスのデバイス スタックにアタッチする必要があります。

1.  呼び出す[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)次のように、現在のデバイス用に FDO を作成します。

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

    入力パラメーターを[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)に渡されたドライバー オブジェクトへのポインターは、 *AddDevice*ルーチン、NULL の代わりにデバイスの拡張機能のサイズデバイス名、およびデバイスのシステム定義の種類 (ファイル\_デバイス\_バッテリ)。 バッテリ miniclass ドライバーに 0 を指定できます、 *DeviceCharacteristics*パラメーターで、これらのドライバーには使用されません。 複数のスレッドは、miniclass ドライバーが FALSE に渡すために、バッテリの I/O 要求を送信できるとして、*排他*パラメーター。 **IoCreateDevice**作成 FDO へのポインターを返します。

2.  返される FDO では、フラグとスタックのサイズを設定します。 以下に例を示します。

    ```cpp
    Fdo->Flags |= DO_BUFFERED_IO;
    Fdo->Flags |= DO_POWER_PAGABLE;
    Fdo->StackSize = Pdo->StackSize + 2;
    ```

    設定は\_バッファーに格納された\_IO フラグは、バッファー内の I/O Irp を使用する miniclass ドライバーを使用します。 設定は\_POWER\_ページング可能なフラグは、ドライバーがページング可能な IRQL で電源 Irp を取得できないことを示します。 &gt;= ディスパッチ\_レベル。 最後に、バッテリの Irp では、追加のスタックの場所が必要とするため miniclass ドライバー設定する必要があります**StackSize** pdo スタック サイズの合計の 2 つのドライバーが IRP PDO までを渡せるようにします。

3.  デバイスの拡張機能には、デバイスの PDO を FDO、デバイスの種類、デバイス名、およびその他の必要な状態へのポインターへのポインターを格納します。 例:

    ```cpp
    NewBatt = (PNEW_BATT) Fdo->DeviceExtension;
    NewBatt->Type = NEW_BATTERY_TYPE;
    NewBatt->Fdo = Fdo;
    NewBatt->Pdo = Pdo;
    NewBatt->IsCacheValid = FALSE;
    ```

    例では、デバイスの拡張機能で FDO と PDO へのポインターを格納します。 (PnP マネージャーとして PDO へのポインターを提供する、 *PhysicalDeviceObject*へのポインター入力*AddDevice*)。さらに、上記の例の追跡、独自のバッテリのタイプ (新規\_バッテリ\_この仮定 miniclass ドライバーで定義されている型) およびキャッシュされた情報が有効かどうか。

    デバイスの拡張機能に格納された情報を指定します。 たとえば、スマート バッテリ ドライバー可能性があります、数を保持、バッテリのバッテリ セレクターが存在するかどうかと、必要に応じて、そのバッテリ セレクターに関する情報を示すブール値。

4.  呼び出す[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)デバイス スタックを FDO をアタッチし、ポインターを格納返された、次のようにします。

    ```cpp
    NewBatt->LowerDO = IoAttachDeviceToDeviceStack(Fdo,Pdo);
    ```

    呼び出しでは、この例で、デバイスの拡張機能に格納する次の下位のデバイス オブジェクトにポインターを返します。

5.  オフにします\_デバイス\_FDO でフラグを次のように初期化します。

    ```cpp
    Fdo->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

    オフ\_デバイス\_初期化フラグは、デバイス履歴の上位にコンポーネントによって後で開かれるデバイス オブジェクトを使用します。

 

 




