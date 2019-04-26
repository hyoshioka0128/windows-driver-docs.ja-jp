---
title: ドライバーの読み込み可能なこと
description: ドライバーをロードするためには、必要なドライバー コールバック ルーチン (DriverEntry) を登録する関数、デバイス スタック (DeviceAdd) にドライバーをアタッチする関数および (が不要になったときに、ドライバーをアンロードする関数を追加する必要があります。DriverUnload)。
ms.assetid: 6BEB7CBC-0179-41B3-BD3D-126290940768
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 522791f3f858b57ea2ced94220ae02b6a944619b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345138"
---
# <a name="make-the-driver-loadable"></a>ドライバーの読み込み可能なこと


ドライバーをロードするためには、必要なドライバーのコールバック ルーチンを登録する関数を追加する必要があります (**DriverEntry**)、デバイス スタックにドライバーをアタッチする関数 (**DeviceAdd**)、および不要になったときに、ドライバーをアンロード関数 (**DriverUnload**)。

次のセクションでは、読み込み可能なセンサーには、ドライバーを作成する方法を表示するためのテスト ケースとして、ADXL345 加速度計から開発されたドライバーのサンプル コード スニペットを使用します。 既に同意していないに移動、 [ADXL345Acc サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc)github の説明と共に利用できるようにします。

これらのコード スニペットは、センサー ドライバー ファイルの重要なセクションの一部を強調表示します。 ドライバーのしくみを理解して、センサーのこれらのファイルをカスタマイズする方法を把握することができる、全体のすべてのドライバー ファイルを確認する必要があります。

## <a name="register-the-driver---driverentry"></a>ドライバー - DriverEntry を登録します。


1. 開いて、 *driver.cpp* NTSTATUS DriverEntry 始まるコード ブロックを検索し、ファイルします。 **DriverEntry**関数を構成し、初期化、DriverObject センサー ドライバーを登録します。 また、この関数は、WPP トレースを使用してログ記録を初期化します。
2. 内で**DriverEntry**、次のコードを検索します。
   ```cpp
   WPP_INIT_TRACING(DriverObject, NULL);
   ```

このコードでは、ドライバーのログ記録を構成します。

3. 検索、WDF\_ドライバー\_CONFIG\_INIT ステートメント。 WDF\_ドライバー\_CONFIG\_INIT 関数を呼び出して設定を**DeviceAdd**コールバック。
   ```cpp
   WDF_DRIVER_CONFIG_INIT(&DriverConfig, ADXL345AccDevice::OnDeviceAdd);
   ```

4. 検索するブロックのコードから始まります NTSTATUS 状態 WdfDriverCreate を = です。
   ```cpp
   NTSTATUS Status = WdfDriverCreate(DriverObject, RegistryPath, WDF_NO_OBJECT_ATTRIBUTES, &DriverConfig, WDF_NO_HANDLE);
   ```

WdfDriverCreate 関数は、ドライバー オブジェクトを初期化するために使用されます。

5. 閉じる、 *driver.cpp*ファイル。
   ## <a name="set-up-the-device-object---deviceadd"></a>デバイス オブジェクト - DeviceAdd 設定します。


6. 開いて、 *device.cpp*ファイルを検索し、 **OnDeviceAdd**関数。 この関数は、デバイス スタックにドライバーをアタッチし、デバイスにデバイスごとの context 構造体を割り当てます。 **OnDeviceAdd**は通常、ドライバーに実行される 2 つ目の呼び出し中に呼び出されます。 ドライバーを開発するときは、PnP、電源管理、および I/O を処理するコードを含めることもできます。
7. 次のコードを検索します。
   ```cpp
   // Create WDFOBJECT for the sensor
   WDF_OBJECT_ATTRIBUTES attributes;
   WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(WDFDRIVER Driver, &attributes, ADXL345AccDevice);
   ```

このコードは、デバイス オブジェクトの種類 ADXL345AccDevice の context 構造体を設定します。

3. 次のコードを検索します。
   ```cpp
   // Call the framework to create the device
   NTSTATUS Status = WdfDeviceCreate(&pAccDeviceInit, &FdoAttributes, &Device);
   ```

この関数は、WDFDEVICE オブジェクトの作成に使用されます。 WDF では、デバイス オブジェクトを作成し、しを ADXL345 加速度計のコンテキストを割り当てます。

4. 閉じる、 *device.cpp*ファイル。
   ## <a name="unload-the-driver---driverunload"></a>ドライバー - DriverUnload をアンロードします。


5. 開いて、 *driver.cpp*ファイルを見つけて、 **OnDriverUnload**関数。 この関数は、IO マネージャーがメモリからドライバーをアンロードした後にクリーンアップを実行するに使用されます。
6. 次のコードを検索します。
   ```cpp
   WPP_CLEANUP(WdfDriverWdmGetDriverObject(Driver));
   ```

このコードは、WPP 診断トレースをオフにします。

 

 




