---
title: DriverEntry の移植
description: DriverEntry の移植
ms.assetid: E880A45A-136C-480E-BE66-B61558F98227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 965aa4e449344bb390ddb7dbae3645b57f7b7b66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842256"
---
# <a name="porting-driverentry"></a>DriverEntry の移植


WDM とフレームワークベースのドライバーの両方で、 [**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数がプライマリエントリポイントになります。 関数プロトタイプは、両方のモデルで同じです。 WDM ドライバーでは、ドライバーが最初にメモリに読み込まれるときに**Driverentry**を呼び出します。 DriverEntry は、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンへのポインターを[ **\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)の AddDevice フィールドに設定します。これは、ドライバーのドライバーの **&gt;** フィールドにあり、 **MajorFunction**の i/o ディスパッチルーチンへのポインターを設定します。ドライバー\_オブジェクト構造体の配列。次に、を返します。 フレームワークベースのドライバーでは、ドライバーの読み込み時に、システムがフレームワークの内部**Fxdriverentry**関数を呼び出します。 この内部関数は、フレームワークを初期化し、ドライバーの**Driverentry**関数を呼び出します。 **Driverentry**は、次の例に示すように、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックへのポインターを設定し、 [**wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出して wdfdriver オブジェクトを作成します。

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject
    IN PUNICODE_STRING RegistryPath
    )
{
    WDF_DRIVER_CONFIG config;

    WDF_DRIVER_CONFIG_INIT( &config,
                              ToasterEvtDeviceAdd );
    status = WdfDriverCreate(
                 DriverObject,
                 RegistryPath,
                 WDF_NO_OBJECT_ATTRIBUTES,
                 &config,
                 WDF_NO_HANDLE
             );

    return STATUS_SUCCESS;
}
```

**Driverentry**は、ルックアサイドリストの作成やトレースの初期化など、ドライバーが必要とするすべてのグローバルデータまたはリソースを初期化します。 [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)では WDFDRIVER オブジェクトへのハンドルが返されますが、WDM ドライバーでは**driverentry**ルーチンに渡されたドライバー\_オブジェクトポインターが保持されない可能性があるのと同様に、ドライバーはこのハンドルを保持しません。 理由は同じです。ドライバーオブジェクトへのポインターを使用するドライバーはごくわずかです。

 

 





