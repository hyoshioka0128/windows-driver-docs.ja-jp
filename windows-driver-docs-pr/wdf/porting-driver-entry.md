---
title: DriverEntry の移植
description: DriverEntry の移植
ms.assetid: E880A45A-136C-480E-BE66-B61558F98227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd941bc36d8d09cff1fd5b3c9a6d55001c787ad
ms.sourcegitcommit: ead145093395141164ec18a4764b19472ea9ff4b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65760599"
---
# <a name="porting-driverentry"></a>DriverEntry の移植


WDM と framework ベースのドライバーの両方で、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)関数は、主なエントリ ポイント。 関数プロトタイプでは、両方のモデルで同じです。 システムの呼び出し、WDM ドライバーの**DriverEntry**ドライバーがメモリに読み込まれたとき。 DriverEntry のポインターを設定するドライバーの[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)で日常的な**DriverExtension -&gt;AddDevice**のフィールド、 [ **ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)構造、その I/O ディスパッチ ルーチンへのポインターのセット、 **MajorFunction**ドライバーの配列\_オブジェクトの構造、し、返します。 フレームワーク ベースのドライバーでは、システムで、フレームワークの内部**FxDriverEntry**ドライバーの読み込み時に機能します。 この内部関数が、フレームワークを初期化し、呼び出してドライバーの**DriverEntry**関数。 **DriverEntry**ドライバーへのポインターを設定[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバックと呼び出し[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)に次の例のように、WDFDRIVER オブジェクトを作成します。

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

**DriverEntry**もルック アサイド リストの作成やトレースの初期化など、ドライバーを必要とするすべてのグローバルなデータやリソースを初期化します。 反[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175) WDM ドライバーがドライバーが保持されないと同様、ドライバーが、このハンドルを保持しません、WDFDRIVER を識別するハンドルでオブジェクトを返します\_オブジェクト ポインターを渡された、 **DriverEntry**ルーチン。 理由は、同じ: だけで、いくつかのドライバーがドライバー オブジェクトへのポインターを使用します。

 

 





