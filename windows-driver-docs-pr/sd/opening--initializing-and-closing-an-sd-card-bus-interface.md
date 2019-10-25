---
title: SD カードのバス インターフェイスを開く、初期化する、および閉じる
description: SD カードのバス インターフェイスを開く、初期化する、および閉じる
ms.assetid: 986a352e-c479-444d-9c65-7958dd638bbb
keywords:
- SD WDK バス, オープンインターフェイス
- SD WDK バス、初期化 (インターフェイスを)
- SD WDK バス、終了インターフェイス
- SD バスインターフェイスを初期化しています
- SdBusOpenInterface
- SDBUS_INTERFACE_STANDARD
- インターフェイス WDK SD bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f4004d0ce0fd952f5c9613ed43df59fd0d7ee2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824720"
---
# <a name="opening-initializing-and-closing-an-sd-card-bus-interface"></a>SD カードのバス インターフェイスを開く、初期化する、および閉じる


セキュアデジタル (SD) デバイスドライバーは、管理対象のデバイスまたはホストコントローラーと対話するために、SD bus インターフェイスを開いて初期化する必要があります。 このためには、SD バスライブラリを呼び出す必要があります。これには、 [**Sdbusopeninterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface)の呼び出しの後に、バスドライバーによって提供されるルーチンを呼び出して、インターフェイスを初期化します。 **Sdbusopeninterface**は、 [**sdbus\_インターフェイス\_標準**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))構造体の**InterfaceReference**メンバー内のインターフェイスを初期化するルーチンへのポインターを返します。 デバイスドライバーは、この初期化ルーチンを呼び出して、バスドライバーに割り込み通知コールバックルーチンへのポインターを提供する必要があります。 バスドライバーは、このコールバックを使用して、ハードウェアの割り込みをデバイスドライバーに通知します。 SD バスインターフェイスを初期化するルーチンの詳細については、「 [**PSDBUS\_INITIALIZE\_interface\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)」を参照してください。 通常、デバイスドライバーは、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン内から SD bus インターフェイスを開き、初期化します。

次のコード例は、SD bus インターフェイスを開いて初期化する呼び出しのシーケンスを示しています。

```cpp
  status = SdBusOpenInterface (pDevExt->UnderlyingPDO,
    &pDevExt->BusInterface,
    sizeof(SDBUS_INTERFACE_STANDARD),
    SDBUS_INTERFACE_VERSION);

  if (NT_SUCCESS(status)) {
    SDBUS_INTERFACE_PARAMETERS interfaceParameters = {0};
    interfaceParameters.Size = 
      sizeof(SDBUS_INTERFACE_PARAMETERS);
    interfaceParameters.TargetObject = 
      DeviceExtension->TargetObject;
    interfaceParameters.DeviceGeneratesInterrupts = TRUE;
    interfaceParameters.CallbackRoutine = pMyDriverCallback;
    status = STATUS_UNSUCCESSFUL;
    if (DeviceExtension->BusInterface.InitializeInterface) {
      status = (pDevExt->BusInterface.InitializeInterface)
        (pDevExt->BusInterface.Context, &interfaceParameters);
    }
      }
```

このコード例では、デバイスドライバーが**Sdbusopeninterface**を呼び出してインターフェイスを開き、バスドライバーがデバイス拡張機能 (**deviceextension-&gt;Businterface. initializeinterface) に初期化ルーチンへのポインターを格納します。** ). **Sdbusopeninterface**が返された後、ドライバーはデバイスの拡張機能からこのポインターを取得します。 次に、ドライバーは、独自の割り込みコールバックルーチン**Pmydrivercallback**へのポインターを、 [**SDBUS\_インターフェイス\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))構造体に書き込み、この構造体を初期化ルーチンに渡します。

また、デバイスドライバーは、sdbus **Openinterface**が\_標準構造体の sdbus\_インターフェイスの**コンテキスト**メンバーで返すコンテキスト情報も取得する必要があります。 ドライバーは SD bus インターフェイスルーチンを呼び出すたびに、このコンテキストデータを渡す必要があります。

### <a name="closing-an-sd-interface"></a>SD インターフェイスを閉じる

SD インターフェイスを閉じるには、SDBUS\_\_インターフェイスの**Interfacedereference 参照**メンバーでルーチンを呼び出すことによって、ドライバーがインターフェイスを逆参照する必要があります。この場合、標準構造体は、によって割り当てられたすべての**リソースを解放します。SdBusOpenInterface**ルーチン。 SD デバイスドライバーは、次のいずれかの Irp を受信したときに、開いているすべての SD インターフェイスを閉じる必要があります。

[**IRP\_\_クエリ\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_\_驚く\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

次のコード例は、ドライバーが SD カードバスインターフェイスを逆参照する方法を示しています。

```cpp
if (pDevExt->BusInterface.InterfaceDereference) {
    (pDevExt->BusInterface.InterfaceDereference) (pDevExt->BusInterface.Context);
    RtlZeroMemory(&pDevExt->BusInterface, sizeof(SDBUS_INTERFACE_STANDARD));
}
```

**Sdbusopeninterface**呼び出しは、sdbus\_インターフェイス\_標準構造体のインターフェイス逆参照ルーチンへのポインターを格納します。 ただし、ルーチンの呼び出しを試行する前に、ドライバーはポインターが**NULL**でないことを確認する必要があります。

 

 




