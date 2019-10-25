---
title: 一般 I/O ターゲットの初期化
description: 一般 I/O ターゲットの初期化
ms.assetid: c5d5b589-09a3-4f58-83bf-2876b37b0937
keywords:
- 一般的な i/o ターゲット WDK KMDF、初期化
- 一般的な i/o ターゲットの初期化 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59b77265dbbcc915560afbc9a40b92bdb2fac301
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844778"
---
# <a name="initializing-a-general-io-target"></a>一般 I/O ターゲットの初期化





このフレームワークは、ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すときに、デバイスのローカル i/o ターゲットを初期化します。 デバイスのローカル i/o ターゲットへのハンドルを取得するために、ドライバーは[**Wdfdevicegetiotarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)を呼び出します。

ほとんどのドライバーは、ローカルの i/o ターゲットにのみ要求を送信します。

デバイスのリモート i/o ターゲットを初期化するには、ドライバーは次のことを行う必要があります。

1.  [**Wdfiotargetcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate)を呼び出して、i/o ターゲットオブジェクトを作成します。

2.  [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出して、i/o ターゲットを開き、ドライバーが要求を送信できるようにします。

ドライバーは、 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出すと、通常、[オブジェクト名](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-names)を表す Unicode 文字列を指定することによって、リモート i/o ターゲットを識別します。 この名前は、デバイス、ファイル、またはデバイスのインターフェイスを識別できます。 フレームワークは、オブジェクト名をサポートするドライバースタックの先頭に i/o 要求を送信します。

ほとんどの場合、ドライバーは、Windows Driver Model (WDM)[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造へのポインターを指定することによって、リモート i/o ターゲットを識別することがあります。 このポインターは、呼び出し元のドライバーのスタック内の別のドライバーを識別します。 フレームワークベースのドライバーは、他のドライバーの**デバイス\_オブジェクト**構造にアクセスすることはほとんどないため、この手法を使用することはほとんどありません。

次の例では、Ndisedge サンプルドライバーが上記の手法を使用して、リモート i/o ターゲットを作成し、開く方法を示します。

```cpp
status = WdfIoTargetCreate(Adapter->WdfDevice,
                        WDF_NO_OBJECT_ATTRIBUTES,
                        &Adapter->IoTarget);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetCreate failed 0x%x\n",
               status));
        return status;
    }

    WDF_IO_TARGET_OPEN_PARAMS_INIT_CREATE_BY_NAME(&openParams,
                                &fileName,
                                STANDARD_RIGHTS_ALL
                                );

    status = WdfIoTargetOpen(Adapter->IoTarget,
                        &openParams);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetOpen failed 0x%x\n", status));
        return status;
    }
```

 

 





