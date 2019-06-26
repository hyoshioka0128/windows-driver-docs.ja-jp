---
title: DriverEntry の移植
description: DriverEntry の移植
ms.assetid: E880A45A-136C-480E-BE66-B61558F98227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88945db7afe17898f921bae61e7fd3c765f1771b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379645"
---
# <a name="porting-driverentry"></a>DriverEntry の移植


WDM と framework ベースのドライバーの両方で、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)関数は、主なエントリ ポイント。 関数プロトタイプでは、両方のモデルで同じです。 システムの呼び出し、WDM ドライバーの**DriverEntry**ドライバーがメモリに読み込まれたとき。 DriverEntry のポインターを設定するドライバーの[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)で日常的な**DriverExtension -&gt;AddDevice**のフィールド、 [ **ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)構造、その I/O ディスパッチ ルーチンへのポインターのセット、 **MajorFunction**ドライバーの配列\_オブジェクトの構造、し、返します。 フレームワーク ベースのドライバーでは、システムで、フレームワークの内部**FxDriverEntry**ドライバーの読み込み時に機能します。 この内部関数が、フレームワークを初期化し、呼び出してドライバーの**DriverEntry**関数。 **DriverEntry**ドライバーへのポインターを設定[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックと呼び出し[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)に次の例のように、WDFDRIVER オブジェクトを作成します。

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

**DriverEntry**もルック アサイド リストの作成やトレースの初期化など、ドライバーを必要とするすべてのグローバルなデータやリソースを初期化します。 反[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate) WDM ドライバーがドライバーが保持されないと同様、ドライバーが、このハンドルを保持しません、WDFDRIVER を識別するハンドルでオブジェクトを返します\_オブジェクト ポインターを渡された、 **DriverEntry**ルーチン。 理由は、同じ: だけで、いくつかのドライバーがドライバー オブジェクトへのポインターを使用します。

 

 





