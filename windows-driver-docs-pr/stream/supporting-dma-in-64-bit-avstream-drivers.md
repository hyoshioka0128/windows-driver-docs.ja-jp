---
title: 64 ビット AVStream ドライバーの DMA のサポート
description: 64 ビット AVStream ドライバーの DMA のサポート
ms.assetid: 1173a83f-8d9e-4678-bfb5-f2fb91e827be
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA サービス WDK AVStream
- ダイレクトメモリアクセス WDK AVStream
- 64-bit WDK AVStream
- 32ビットアドレス可能なデバイス WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f3064a9d8cce9a3df542acfb3e97a686f669b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837670"
---
# <a name="supporting-dma-in-64-bit-avstream-drivers"></a>64 ビット AVStream ドライバーの DMA のサポート





AVStream では、32ビットおよび64ビットのアドレス指定可能なデバイスで DMA がサポートされています。

Win64 プラットフォーム用にコンパイルされたすべてのドライバーは、 [**KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)ではなく[**Iksdevicefunctions:: RegisterAdapterObjectEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-iksdevicefunctions-registeradapterobjectex)を使用する必要があります。

**Iksdevicefunctions:: RegisterAdapterObjectEx**は、Microsoft Windows SERVER 2003 SP1 以降でのみ使用できます。

次のコード例は、x64 ベースのクライアントリリースと32ビットの両方のプラットフォームで DMA をサポートする方法を示しています。

```cpp
NTSTATUS MyDeviceStart (...) {
// Get the DMA adapter object and store it in the Context member of the I/O stack location.
Context -> AdapterObject = IoGetDmaAdapter (
Device -> PhysicalDeviceObject,
&DeviceDesc,
&Context -> NumberOfMapRegisters
);

PUNKNOWN DeviceUnk =
KsDeviceGetOuterUnknown (
Device
);

// Register the DMA adapter with AVStream
IKsDeviceFunctions *DeviceFunctions;
NTSTATUS Status = DeviceUnk -> QueryInterface (
__uuidof (IKsDeviceFunctions),
(PVOID *)&DeviceFunctions
);

// Conditionally, call IksDeviceFunctions::RegisterAdapterObjectEx, 
// which will not break downlevel load compatibility.

if (NT_SUCCESS (Status)) {
DeviceFunctions -> RegisterAdapterObjectEx (
Context -> AdapterObject,
&DeviceDesc,
Context -> NumMapRegisters,
MAX_MAPPING,
sizeof (KSMAPPING)
);
DeviceFunctions -> Release ();
}

// If this call fails, call KsDeviceRegisterAdapterObject to
// preserve downlevel load compatibility.
else {
KsDeviceRegisterAdapterObject (
Device,
Context -> AdapterObject,
MAX_MAPPING,
sizeof (KSMAPPING)
);
}
...
```

このコード例は、64ビットと32ビットのプラットフォームで動作します。 ドライバーが**Iksdevicefunctions:: RegisterAdapterObjectEx**を見つけられない場合でも、 **KsDeviceRegisterAdapter**を呼び出します。

さらに、64ビット AVStream ドライバーを作成する場合は、保持されている同時実行フレームロックの数を最小限に抑えます。 ミニドライバーが最初にフレームをロックしたときに AVStream によってスキャッター/ギャザーマッピングが生成されるため、このガイドラインに従っていない場合は、ドライバーでリソースが不足する可能性があります。 特に、32ビットカードを使用する Win64 プラットフォームで実行するドライバーを作成する場合は、同時ロックの数を増やすと、メモリが不足しているためにロックが失敗する可能性が高くなります。

 

 




