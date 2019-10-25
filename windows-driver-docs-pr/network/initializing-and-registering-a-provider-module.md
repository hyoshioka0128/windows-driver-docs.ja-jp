---
title: プロバイダー モジュールの初期化と登録
description: プロバイダー モジュールの初期化と登録
ms.assetid: 967271ce-e4f5-45ce-9249-746d2fe698c1
keywords:
- プロバイダーモジュール WDK ネットワークモジュールレジストラー, 初期化
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、登録
- プロバイダーモジュールの登録
- プロバイダーモジュールの初期化
- NmrRegisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02921de7125176883d16891d7c0295eeea1cf3ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824482"
---
# <a name="initializing-and-registering-a-provider-module"></a>プロバイダー モジュールの初期化と登録


プロバイダーモジュールは、ネットワークモジュールレジストラー (NMR) に登録する前に、いくつかのデータ構造を初期化する必要があります。 これらの構造体には、 [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造体、 [**NPI\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_provider_characteristics)構造、 [**NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)構造 (NPI 内に含まれる) が含まれ\_プロバイダー\_特性の構造) と、プロバイダーモジュールによって定義された構造体。プロバイダーモジュールの登録コンテキストに使用されます。

プロバイダーモジュールが、NPI 固有のプロバイダーの特性を定義する[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)のプロバイダーとして自身を NMR に登録する場合、プロバイダーモジュールはプロバイダーの特性のインスタンスを初期化する必要もあります。NPI によって定義される構造体。

プロバイダーモジュールが NMR に登録されている限り、これらのデータ構造はすべて有効であり、メモリ内に常駐している必要があります。

たとえば、"EXNPI" NPI で、ヘッダーファイル Exnpi に次のものが定義されているとします。

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

次の例は、EXNPI NPI のプロバイダーとして登録するプロバイダーモジュールが、これらのすべてのデータ構造を初期化できる方法を示しています。

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

プロバイダーモジュールは通常、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内で自身を初期化します。 プロバイダーモジュールの主な初期化タスクは次のとおりです。

-   [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を指定します。 オペレーティングシステムは、プロバイダーモジュールがシステムからアンロードされるときに、この関数を呼び出します。 プロバイダーモジュールが unload 関数を提供していない場合、プロバイダーモジュールをシステムからアンロードすることはできません。

-   [**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)関数を呼び出して、プロバイダーモジュールを NMR に登録します。

次に、例を示します。

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

プロバイダーモジュールが複数の NPI のプロバイダーである場合は、データ構造の独立したセットを初期化し、サポートする各 NPI に対して[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)を呼び出す必要があります。 ネットワークモジュールがプロバイダーモジュールとクライアントモジュール (つまり、1つの NPI のプロバイダーと別の NPI のクライアント) の両方である場合、プロバイダーインターフェイス用とクライアントインターフェイス用の2つの独立したデータ構造体を初期化する必要があります。を呼び出し、 **NmrRegisterProvider**と[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)の両方を呼び出します。

プロバイダーモジュールは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内から[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)を呼び出すためには必要ありません。 たとえば、プロバイダーモジュールが複雑なドライバーのサブコンポーネントである場合、プロバイダーモジュールの登録は、プロバイダーモジュールのサブコンポーネントがアクティブ化されている場合にのみ発生することがあります。

プロバイダーモジュールの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数の実装の詳細については、「[プロバイダーモジュールのアンロード](unloading-a-provider-module.md)」を参照してください。

 

 





