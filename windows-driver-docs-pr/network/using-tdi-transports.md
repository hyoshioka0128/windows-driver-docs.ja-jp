---
title: TDI トランスポートの使用
description: TDI トランスポートの使用
ms.assetid: 58fb5e62-e15d-4f15-8eb3-3e302ea08c4f
keywords:
- TDI は、WDK Winsock Kernel を転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2753f2b49cde398da3caba407475f72b60dc9cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372479"
---
# <a name="using-tdi-transports"></a>TDI トランスポートの使用


Winsock カーネル (WSK) サブシステムを使用するためのサポートを提供します[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))トランスポート。 使用して、WSK TDI トランスポートを使用するには[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)WSK アプリケーション アドレス ファミリ、ソケットの種類の組み合わせをマップする必要があり、TDI ごとのプロトコルが転送に関連するデバイスの名前に使用します。これらのそれぞれの TDI を転送します。 WSK アプリケーションは、アドレス ファミリ、ソケットの種類の組み合わせをマップし、TDI のデバイス名にプロトコルのトランスポートを使用して、 [ **WSK\_TDI\_DEVICENAME\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-tdi-devicename-mapping)クライアント管理の操作。

次のコード例では、TDI トランスポートのデバイス名を WSK アプリケーションがアドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせをマップする方法を示します。

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

WSK アプリケーションは、ソケットを作成する前に TDI トランスポートのデバイス名にアドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせをマップする必要があります。 WSK アプリケーションでは、アドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名にマップされることが正常に後、アプリケーションは、マップされた TDI トランスポートを使用する新しいソケットを作成できます。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

 

 





