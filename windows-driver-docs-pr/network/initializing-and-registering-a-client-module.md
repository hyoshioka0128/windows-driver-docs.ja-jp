---
title: クライアント モジュールの初期化と登録
description: クライアント モジュールの初期化と登録
ms.assetid: 3d0941d0-5a6f-4c6d-b519-af850a8de341
keywords:
- クライアントのモジュールの初期化、WDK ネットワーク モジュール レジストラー
- クライアント モジュールを登録する WDK ネットワーク モジュール レジストラー
- クライアント モジュールを登録します。
- クライアント モジュールを初期化しています
- NmrRegisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f001614b33f880a815b216e109e03544f852df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381286"
---
# <a name="initializing-and-registering-a-client-module"></a>クライアント モジュールの初期化と登録


クライアント モジュールは、ネットワーク モジュール レジストラー (NMR) で登録にする前に、さまざまなデータ構造体を初期化する必要があります。 これらの構造が含まれます、 [ **NPI\_MODULEID** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造、 [ **NPI\_クライアント\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_client_characteristics)構造、 [ **NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance)構造 (、NPI 内に含まれる\_クライアント\_の特性構造)、およびクライアント モジュールの登録のコンテキストに使用されるクライアント モジュールで定義された構造です。

かどうかクライアント モジュールに自らを登録、NMR のクライアントとして、[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md) NPI に固有のクライアントの特性を定義する、クライアント モジュールは、クライアントのインスタンスを初期化する必要がありますもNPI によって定義された特性構造体。

クライアント モジュールは、NMR に登録されている限りは、有効であり、メモリに常駐すべてこれらのデータ構造のままする必要があります。

たとえば、"EXNPI"NPI Exnpi.h のヘッダー ファイルで、次を定義します。

```C++
// EXNPI NPI identifier
const NPIID EXNPI_NPIID = { ... };

// EXNPI client characteristics structure
typedef struct EXNPI_CLIENT_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_CLIENT_CHARACTERISTICS, *PEXNPI_CLIENT_CHARACTERISTICS;
```

EXNPI NPI のクライアントとして自身を登録するクライアント モジュールが初期化これらのデータ構造のすべての方法を次に示します。

```C++
// Include the NPI specific header file
#include "exnpi.h"

// Structure for the client module's NPI-specific characteristics
const EXNPI_CLIENT_CHARACTERISTICS NpiSpecificCharacteristics =
{
  .
  . // The NPI-specific characteristics of the client module
  .
};

// Structure for the client module's identification
const NPI_MODULEID ClientModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the client module
};

// Prototypes for the client module's callback functions
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    );

NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    );

VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    );

// Structure for the client module's characteristics
const NPI_CLIENT_CHARACTERISTICS ClientCharacteristics =
{
  0,
  sizeof(NPI_CLIENT_CHARACTERISTICS),
  ClientAttachProvider,
  ClientDetachProvider,
  ClientCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &EXNPI_NPIID,
    &ClientModuleId,
    0,
    &NpiSpecificCharacteristics
  }
};

// Context structure for the client module's registration
typedef struct CLIENT_REGISTRATION_CONTEXT_ {
  .
  . // Client-specific members
  .
} CLIENT_REGISTRATION_CONTEXT, *PCLIENT_REGISTRATION_CONTEXT;

// Structure for the client's registration context
CLIENT_REGISTRATION_CONTEXT ClientRegistrationContext =
{
  .
  . // Initial values for the registration context
  .
};
```

クライアントのモジュールが通常初期化自体内でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 モジュールのクライアントのメインの初期化タスクは次のとおりです。

-   指定、 [**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数。 オペレーティング システムは、クライアント モジュールがシステムからアンロードされるときに、この関数を呼び出します。 クライアント モジュールはアンロード、関数を提供していない場合、クライアント モジュールは、システムからアンロードすることはできません。

-   呼び出す、 [ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient) NMR をクライアント モジュールを登録する関数。

例:

```C++
// Prototype for the client module's unload function
VOID
  Unload(
    PDRIVER_OBJECT DriverObject
    );

// Variable to contain the handle for the registration
HANDLE ClientHandle;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;

  // Specify the unload function
  DriverObject->DriverUnload = Unload;

  .
  . // Other initialization tasks
  .

  // Register the client module with the NMR
  Status = NmrRegisterClient(
    &ClientCharacteristics,
    &ClientRegistrationContext,
    &ClientHandle
    );

  // Return the result of the registration
  return Status;
}
```

データ構造と呼び出しの独立したセットを初期化する必要がありますクライアント モジュールが 1 つ以上の NPI のクライアントの場合は、 [ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient)各 NPI でサポートされるのです。 ネットワーク モジュールがクライアント モジュールとプロバイダー モジュールの両方のかどうか (つまり、NPI の 1 つのクライアントおよび別の NPI のプロバイダー) である 2 つの独立したデータ構造、クライアント インターフェイスおよびプロバイダー インターフェイスのセットを初期化する必要があります、両方を呼び出すと**NmrRegisterClient**と[ **NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider)します。

クライアント モジュールを呼び出す必要はありません[ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient)内からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 たとえば、クライアント モジュールが複雑なドライバーのサブコンポーネントが場合、クライアント モジュールの登録が発生するクライアントのサブコンポーネントのモジュールがアクティブな場合にのみ。

クライアント モジュールの実装の詳細については[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数を参照してください[クライアント モジュールをアンロード](unloading-a-client-module.md)します。

 

 





