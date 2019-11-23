---
title: TDI トランスポートの使用
description: TDI トランスポートの使用
ms.assetid: 58fb5e62-e15d-4f15-8eb3-3e302ea08c4f
keywords:
- TDI トランスポート WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb4f82a3bc0315636a9172092a2579f31f05e73c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842971"
---
# <a name="using-tdi-transports"></a>TDI トランスポートの使用


Winsock カーネル (WSK) サブシステムでは、 [TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))トランスポートの使用がサポートされています。 WSK[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)を介して tdi トランスポートを使用するには、wsk アプリケーションで、使用する各 tdi トランスポートのアドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを、それぞれの tdi トランスポートの関連付けられたデバイス名にマップする必要があります。 WSK アプリケーションは、アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを、 [**wsk\_tdi\_DEVICENAME\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-tdi-devicename-mapping)クライアントコントロール操作を使用して、tdi トランスポートのデバイス名にマップします。

次のコード例は、WSK アプリケーションで、アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを、TDI トランスポートのデバイス名にマップする方法を示しています。

```C++
// Number of TDI mappings
#define MAPCOUNT 2

// Array of TDI mappings
const WSK_TDI_MAP TdiMap[MAPCOUNT] =
{
  {SOCK_STREAM, ..., ..., ...},
  {SOCK_DGRAM, ..., ..., ...}
};

// TDI map info structure
const WSK_TDI_MAP_INFO TdiMapInfo =
{
  MAPCOUNT,
  TdiMap
}

// Function to set the TDI map
NTSTATUS
  SetTdiMap(
    PWSK_APP_BINDING_CONTEXT BindingContext
  )
{
  NTSTATUS Status;

  // Perform client control operation
  Status =
    BindingContext->
      WskProviderDispatch->
        WskControlClient(
          BindingContext->WskClient,
          WSK_TDI_DEVICENAME_MAPPING,
          sizeof(WSK_TDI_MAP_INFO),
          &TdiMapInfo,
          0,
          NULL,
          NULL,
          NULL  // No IRP for this control operation
          );

  // Return status of client control operation
  return Status;
}
```

WSK アプリケーションは、ソケットを作成する前に、アドレスファミリ、ソケットの種類、プロトコルの組み合わせを TDI トランスポートのデバイス名にマップする必要があります。 WSK アプリケーションで、アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせが TDI トランスポートのデバイス名に正常にマップされた後、アプリケーションは、マップされた TDI トランスポートを使用する新しいソケットを作成できます。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

 

 





