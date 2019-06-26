---
title: プロバイダー モジュールの初期化と登録
description: プロバイダー モジュールの初期化と登録
ms.assetid: 967271ce-e4f5-45ce-9249-746d2fe698c1
keywords:
- プロバイダーのモジュールの初期化、WDK ネットワーク モジュール レジストラー
- プロバイダーのモジュールを登録する WDK ネットワーク モジュール レジストラー
- プロバイダーのモジュールを登録します。
- プロバイダーのモジュールを初期化しています
- NmrRegisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2de912ab0becf1fac9a0a78cd98e7ebcd1145bca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381288"
---
# <a name="initializing-and-registering-a-provider-module"></a>プロバイダー モジュールの初期化と登録


ネットワーク モジュール レジストラー (NMR) で登録にする前に、プロバイダー モジュールはさまざまなデータ構造体を初期化する必要があります。 これらの構造が含まれます、 [ **NPI\_MODULEID** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造、 [ **NPI\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_provider_characteristics)構造、 [ **NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance)構造 (、NPI 内に含まれる\_プロバイダー\_特性構造の場合)、およびプロバイダー モジュールの登録のコンテキストに使用されるプロバイダー モジュールで定義された構造です。

かどうか、プロバイダー モジュールに自らを登録、NMR のプロバイダーとして、[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md) NPI に固有のプロバイダーの特性を定義する、プロバイダー モジュールは、プロバイダーのインスタンスを初期化する必要がありますもNPI で定義されている特性構造体。

プロバイダー モジュールは、NMR に登録されている限りは、有効であり、メモリに常駐すべてこれらのデータ構造のままする必要があります。

たとえば、"EXNPI"NPI Exnpi.h のヘッダー ファイルで、次を定義します。

```C++
// EXNPI NPI identifier
const NPIID EXNPI_NPIID = { ... };

// EXNPI provider characteristics structure
typedef struct EXNPI_PROVIDER_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_PROVIDER_CHARACTERISTICS, *PEXNPI_PROVIDER_CHARACTERISTICS;
```

EXNPI NPI のプロバイダーとして登録されたプロバイダー モジュールが初期化これらのデータ構造のすべての方法を次に示します。

```C++
// Include the NPI specific header file
#include "exnpi.h"

// Structure for the provider module's NPI-specific characteristics
const EXNPI_PROVIDER_CHARACTERISTICS NpiSpecificCharacteristics =
{
  .
  . // The NPI-specific characteristics of the provider module
  .
};

// Structure for the provider module's identification
const NPI_MODULEID ProviderModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the provider module
};

// Prototypes for the provider module's callback functions
NTSTATUS
  ProviderAttachClient(
    IN HANDLE NmrBindingHandle,
    IN PVOID ProviderContext,
    IN PNPI_REGISTRATION_INSTANCE ClientRegistrationInstance,
    IN PVOID ClientBindingContext,
    IN CONST VOID *ClientDispatch,
    OUT PVOID *ProviderBindingContext,
    OUT PVOID *ProviderDispatch
    );

NTSTATUS
  ProviderDetachClient(
    IN PVOID ProviderBindingContext
    );

VOID
  ProviderCleanupBindingContext(
    IN PVOID ProviderBindingContext
    );

// Structure for the provider module's characteristics
const NPI_PROVIDER_CHARACTERISTICS ProviderCharacteristics =
{
  0,
  sizeof(NPI_PROVIDER_CHARACTERISTICS),
  ProviderAttachClient,
  ProviderDetachClient,
  ProviderCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &EXNPI_NPIID,
    &ProviderModuleId,
    0,
    &NpiSpecificCharacteristics
  }
};

// Context structure for the provider module's registration
typedef struct PROVIDER_REGISTRATION_CONTEXT_ {
  .
  . // Provider-specific members
  .
} PROVIDER_REGISTRATION_CONTEXT, *PPROVIDER_REGISTRATION_CONTEXT;

// Structure for the provider's registration context
PROVIDER_REGISTRATION_CONTEXT ProviderRegistrationContext =
{
  .
  . // Initial values for the registration context
  .
};
```

プロバイダーのモジュールが通常初期化自体内でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 プロバイダー モジュールの主な初期化タスクは次のとおりです。

-   指定、 [**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数。 オペレーティング システムは、プロバイダー モジュールがシステムからアンロードされるときに、この関数を呼び出します。 プロバイダー モジュールがアンロード、関数を提供していない場合、プロバイダー モジュールは、システムからアンロードすることはできません。

-   呼び出す、 [ **NmrRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider) NMR をプロバイダー モジュールを登録する関数。

例:

```C++
// Prototype for the provider module's unload function
VOID
  Unload(
    PDRIVER_OBJECT DriverObject
   );

// Variable to contain the handle for the registration
HANDLE ProviderHandle;

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

  // Register the provider module with the NMR
  Status = NmrRegisterProvider(
    &ProviderCharacteristics,
    &ProviderRegistrationContext,
    &ProviderHandle
    );

  // Return the result of the registration
  return Status;
}
```

データ構造と呼び出しの独立したセットを初期化する必要があります、プロバイダー モジュールが 1 つ以上の NPI のプロバイダーである場合は、 [ **NmrRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider)各 NPI でサポートされるのです。 ネットワーク モジュールはプロバイダー モジュールとクライアントのモジュールの両方のかどうか (つまり、NPI の 1 つのプロバイダーと別の NPI のクライアント) である 2 つの独立したデータ構造、プロバイダーのインターフェイスと、クライアント インターフェイスのセットを初期化する必要があります、両方を呼び出すと**NmrRegisterProvider**と[ **NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient)します。

プロバイダー モジュールを呼び出す必要はありません[ **NmrRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider)内からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 たとえば、プロバイダー モジュールが複雑なドライバーのサブコンポーネントが場合、プロバイダー モジュールの登録と発生する可能性のみプロバイダー モジュールのサブコンポーネントがアクティブ化します。

プロバイダー モジュールの実装の詳細については[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数を参照してください[プロバイダー モジュールをアンロード](unloading-a-provider-module.md)します。

 

 





