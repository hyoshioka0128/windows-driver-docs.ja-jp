---
title: デバイス オブジェクトの作成
description: デバイス オブジェクトの作成
ms.assetid: 9474e080-b2c3-4c1b-af19-bf269d1c94d4
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、初期化しています
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの初期化
- WDK Windows フィルタ リング プラットフォームのデバイス オブジェクト
- WDM ベース コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- WDF ベース コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdeb8eb4b248d1976be8c70c9b7aa87c67627789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357390"
---
# <a name="creating-a-device-object"></a>デバイス オブジェクトの作成


コールアウト ドライバーは、フィルター エンジンとそのコールアウトを登録する前に、デバイス オブジェクトを作成する必要があります。 コールアウト ドライバーがデバイス オブジェクトを作成する方法は、コールアウト ドライバーを Windows Driver Model (WDM) または Windows Driver Frameworks (WDF) に基づくかどうかによって異なります。

### <a name="wdm-based-callout-drivers"></a>WDM ベース コールアウト ドライバー

呼び出すことによって、デバイス オブジェクトを作成、コールアウト ドライバーは、WDM に基づいている場合、 [ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)関数。 例:

```C++
PDEVICE_OBJECT deviceObject;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS status;

  ...

  // Create a device object
 status =
 IoCreateDevice(
 DriverObject,
      0,
      NULL,
      FILE_DEVICE_UNKNOWN,
      FILE_DEVICE_SECURE_OPEN,
      FALSE,
      &deviceObject
      );

  ...

 return status;
}
```

### <a name="wdf-based-callout-drivers"></a>WDF ベース コールアウト ドライバー

呼び出して framework デバイス オブジェクトを作成、コールアウト ドライバーは WDF に基づいている場合、 [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)関数。 そのコールアウト フィルター エンジンに登録するには、WDF ベースのコールアウト ドライバーは、framework デバイス オブジェクトに関連付けられている WDM デバイス オブジェクトへのポインターを取得する必要があります。 WDF ベースのコールアウト ドライバーが呼び出すことによってこの WDM デバイス オブジェクトへのポインターを取得、 [ **WdfDeviceWdmGetDeviceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff546942)関数。 次に、例を示します。

```C++
WDFDEVICE wdfDevice;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  WDFDRIVER driver;
  PWDFDEVICE_INIT deviceInit;
  PDEVICE_OBJECT deviceObject;
  NTSTATUS status;

  ...

  // Allocate a device initialization structure
 deviceInit =
 WdfControlDeviceInitAllocate(
    driver;
    &SDDL_DEVOBJ_KERNEL_ONLY
    );

  // Set the device characteristics
 WdfDeviceInitSetCharacteristics(
    deviceInit,
    FILE_DEVICE_SECURE_OPEN,
    FALSE
    );

  // Create a framework device object
 status =
 WdfDeviceCreate(
    &deviceInit,
    WDF_NO_OBJECT_ATTRIBUTES,
    &wdfDevice
    );

  // Check status
 if (status == STATUS_SUCCESS) {

    // Initialization of the framework device object is complete
    WdfControlFinishInitializing(
      wdfDevice
    );

    // Get the associated WDM device object
    deviceObject = WdfDeviceWdmGetDeviceObject(wdfDevice);
  }

  ...

 return status;
}
```

 

 





