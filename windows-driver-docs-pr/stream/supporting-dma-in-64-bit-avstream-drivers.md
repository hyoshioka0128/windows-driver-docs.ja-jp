---
title: 64 ビット AVStream ドライバーの DMA のサポート
description: 64 ビット AVStream ドライバーの DMA のサポート
ms.assetid: 1173a83f-8d9e-4678-bfb5-f2fb91e827be
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA は、WDK AVStream をサービスします。
- ダイレクト メモリ アクセスの WDK AVStream
- 64 ビットの WDK AVStream
- 32 ビットのアドレス指定可能なデバイス WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2279137fe23ca5aff81367ddfb71041d68b264d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377774"
---
# <a name="supporting-dma-in-64-bit-avstream-drivers"></a>64 ビット AVStream ドライバーの DMA のサポート





AVStream では、32 ビットおよび 64 ビットのアドレス指定可能なデバイスで DMA をサポートしています。

Win64 プラットフォームを使用する必要があります用にコンパイルされたすべてのドライバー [ **IKsDeviceFunctions::RegisterAdapterObjectEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-iksdevicefunctions-registeradapterobjectex)の代わりに[ **KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdeviceregisteradapterobject).

**IKsDeviceFunctions::RegisterAdapterObjectEx**は Microsoft Windows Server 2003 SP1 で使用可能な以降のみです。

次のコード例では、x64 ベースのクライアントのリリースと 32 ビット プラットフォームの両方で DMA をサポートする方法を示します。

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

このコード例は、32 ビットと 64 ビット プラットフォームで動作します。 ドライバーが見つからない場合**IKsDeviceFunctions::RegisterAdapterObjectEx**、呼び出しがまだ**KsDeviceRegisterAdapter**します。

さらに、64 ビットの AVStream ドライバーを作成するときは、保持されているロックを同時実行のフレームの数を最小限に抑えます。 ミニドライバーは最初のフレームをロックしたときに、AVStream はスキャッター/ギャザーのマッピングを生成するため、ドライバーは、このガイドラインに従わない場合リソースが不足実行可能性があります。 具体的には、低いメモリ バッファーは限られたリソースであるために、ロックが失敗することは、32 ビットのカードで Win64 プラットフォーム上で実行するためのドライバーを作成する場合に同時ロックの数を増やして増加します。

 

 




