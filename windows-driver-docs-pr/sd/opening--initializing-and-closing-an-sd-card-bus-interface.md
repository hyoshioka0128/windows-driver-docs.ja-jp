---
title: SD カードのバス インターフェイスを開く、初期化する、および閉じる
description: SD カードのバス インターフェイスを開く、初期化する、および閉じる
ms.assetid: 986a352e-c479-444d-9c65-7958dd638bbb
keywords:
- SD WDK バス インターフェイスを開く
- SD WDK バス、初期化インターフェイス
- SD WDK バス インターフェイスを閉じる
- SD バス インターフェイスを初期化しています
- SdBusOpenInterface
- SDBUS_INTERFACE_STANDARD
- WDK SD バスをインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55811c6cfb87b3eec6f0eca6b13ac48f79088b5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384503"
---
# <a name="opening-initializing-and-closing-an-sd-card-bus-interface"></a>SD カードのバス インターフェイスを開く、初期化する、および閉じる


デジタル (SD) デバイス ドライバーを開くおよび管理するデバイスやホスト コント ローラーと対話する SD バスのインターフェイスを初期化する必要がありますをセキュリティで保護します。 2 つの SD バス ライブラリの呼び出しが必要です: への呼び出し[ **SdBusOpenInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbusopeninterface)インターフェイスを初期化するバス ドライバーによって提供されるルーチンの呼び出し後にします。 **SdBusOpenInterface**でインターフェイスを初期化するルーチンへのポインターを返します、 **InterfaceReference**のメンバー、 [ **SDBUS\_インターフェイス\_標準**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))構造体。 デバイス ドライバーは、割り込み通知コールバック ルーチンへのポインターをバス ドライバーを提供するには、この初期化ルーチンを呼び出す必要があります。 バス ドライバーでは、このコールバックを使用して、ハードウェア割り込みのデバイス ドライバーに通知します。 SD バスのインターフェイスを初期化するルーチンの詳細については、次を参照してください。 [ **PSDBUS\_初期化\_インターフェイス\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)します。 通常、デバイス ドライバーは開き、内から SD バスのインターフェイスを初期化します、 [ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

次のコード例は、開き SD バスのインターフェイスの初期化呼び出しのシーケンスを示しています。

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

このコード例では、デバイス ドライバーを呼び出す**SdBusOpenInterface** 、インターフェイスを開き、バス ドライバーでは、デバイスの拡張機能の初期化ルーチンへのポインターを格納 (**DeviceExtension-&gt;BusInterface.InitializeInterface**)。 後**SdBusOpenInterface**返します、ドライバーは、デバイスの拡張機能からこのポインターを取得します。 次に、ドライバーは、独自の割り込みコールバック ルーチンにポインターを与えます**pMyDriverCallback、** で、 [ **SDBUS\_インターフェイス\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))構造体であり、初期化ルーチンをこの構造体を渡します。

デバイス ドライバーは、コンテキスト情報を取得する必要がありますもを**SdBusOpenInterface**で返します、**コンテキスト**、SDBUS のメンバー\_インターフェイス\_標準構造体。 ドライバーが SD バス インターフェイス ルーチンを呼び出すたびには、このコンテキストのデータで渡す必要があります。

### <a name="closing-an-sd-interface"></a>SD インターフェイスを閉じる

SD インターフェイスを閉じるには、ドライバー逆参照しなければなりません、インターフェイス、ルーチンを呼び出すことによって、 **InterfaceDereference** 、SDBUS のメンバー\_インターフェイス\_標準の構造にすべてのリソースを解放します。によって割り当てられた、 **SdBusOpenInterface**ルーチン。 SD デバイス ドライバーは Irp を次のいずれかの受信時にすべての開いている SD インターフェイスを閉じる必要があります。

[**IRP\_MN\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_MN\_REMOVE\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

次のコード例では、ドライバーが SD カード バス インターフェイスに逆参照する方法を示しています。

```cpp
if (pDevExt->BusInterface.InterfaceDereference) {
    (pDevExt->BusInterface.InterfaceDereference) (pDevExt->BusInterface.Context);
    RtlZeroMemory(&pDevExt->BusInterface, sizeof(SDBUS_INTERFACE_STANDARD));
}
```

**SdBusOpenInterface**インターフェイスへのポインターを格納、SDBUS でルーチンを逆参照呼び出し\_インターフェイス\_標準構造体。 ただし、ドライバーがポインターでないことを確認する必要があります**NULL**ルーチンを呼び出す前にします。

 

 




