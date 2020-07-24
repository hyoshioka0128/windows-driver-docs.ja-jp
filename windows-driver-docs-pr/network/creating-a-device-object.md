---
title: デバイスオブジェクトの作成 (Windows フィルタリングプラットフォーム)
description: デバイス オブジェクトの作成
ms.assetid: 9474e080-b2c3-4c1b-af19-bf269d1c94d4
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、初期化
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、初期化
- コールアウトドライバーの初期化 WDK Windows フィルタリングプラットフォーム
- デバイスオブジェクト WDK Windows フィルタリングプラットフォーム
- WDM ベースのコールアウトドライバーの WDK Windows フィルタリングプラットフォーム
- WDF ベースのコールアウトドライバー (WDK Windows フィルタリングプラットフォーム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c511695e98662d629345d336c0ee57c3d9e9b2
ms.sourcegitcommit: 53565c07d980307b079a6accf541fd221e623142
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86972155"
---
# <a name="creating-a-device-object-windows-filtering-platform"></a>デバイスオブジェクトの作成 (Windows フィルタリングプラットフォーム)


コールアウトドライバーは、コールアウトをフィルターエンジンに登録する前に、デバイスオブジェクトを作成する必要があります。 コールアウトドライバがデバイスオブジェクトを作成する方法は、コールアウトドライバが Windows Driver Model (WDM) と Windows ドライバフレームワーク (WDF) のどちらに基づいているかによって異なります。

### <a name="wdm-based-callout-drivers"></a>WDM ベースのコールアウトドライバー

コールアウトドライバーが WDM に基づいている場合は、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)関数を呼び出すことによってデバイスオブジェクトを作成します。 次に例を示します。

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

### <a name="wdf-based-callout-drivers"></a>WDF ベースのコールアウトドライバー

コールアウトドライバーが WDF に基づいている場合は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)関数を呼び出すことによって、フレームワークデバイスオブジェクトを作成します。 コールアウトをフィルターエンジンに登録するには、WDF ベースのコールアウトドライバーが、フレームワークデバイスオブジェクトに関連付けられている WDM デバイスオブジェクトへのポインターを取得する必要があります。 WDF ベースのコールアウトドライバーは、 [**WdfDeviceWdmGetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)関数を呼び出すことによって、この WDM デバイスオブジェクトへのポインターを取得します。 次に例を示します。

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

 

 





