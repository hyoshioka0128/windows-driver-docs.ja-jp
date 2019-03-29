---
title: デバイス インターフェイスの使用
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da0b80e0575791256169f7c5ddf7e5328dbc2cf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580741"
---
# <a name="using-device-interfaces"></a>デバイス インターフェイスの使用

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

クライアント ドライバーの呼び出しをユーザー モードから Ioctl を受信する[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)参照文字列を次に示すようにします。

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

参照文字列とデバイスのインターフェイスで開かれたハンドルを要求を送信すると、ユーザー モード アプリケーションには、クライアント ドライバーは、I/O 要求を受信します。  使用することができます[WDF のキュー オブジェクト](../wdf/framework-queue-objects.md)要求を受信した I/O を処理します。  参照文字列を指定しない場合、NDIS は、デバイス インターフェイスへの送信 I/O 要求をインターセプトします。

詳細については、次を参照してください。 [WDF デバイス インターフェイスを使用して](../wdf/using-device-interfaces.md)します。
