---
title: デバイス インターフェイスの使用
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fbe1ef5d1051c3e59f9fbafe7ab117864cb08a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838267"
---
# <a name="using-device-interfaces"></a>デバイス インターフェイスの使用

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

ユーザーモードから Ioctl を受信するために、クライアントドライバーは、次に示すように、参照文字列を使用して[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出します。

```cpp
DECLARE_CONST_UNICODE_STRING(c_RefString, L"MyRefString");
status = WdfDeviceCreateDeviceInterface(
            device, 
            &GUID_MY_DEVICE_INTERFACE, 
            &c_RefString);
if (!NT_SUCCESS(status)) {
    return status;
}
```

ユーザーモードアプリケーションが参照文字列を使用してデバイスインターフェイスで開かれたハンドルに要求を送信すると、クライアントドライバーは i/o 要求を受信します。  [WDF queue オブジェクト](../wdf/framework-queue-objects.md)を使用して、受信 i/o 要求を処理することができます。  参照文字列を指定しない場合、NDIS はデバイスインターフェイスに送信された i/o 要求をインターセプトします。

詳細については、「 [USING WDF Device インターフェイス](../wdf/using-device-interfaces.md)」を参照してください。
