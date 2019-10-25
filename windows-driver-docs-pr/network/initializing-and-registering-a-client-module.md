---
title: クライアント モジュールの初期化と登録
description: クライアント モジュールの初期化と登録
ms.assetid: 3d0941d0-5a6f-4c6d-b519-af850a8de341
keywords:
- クライアントモジュール WDK ネットワークモジュールレジストラー, 初期化
- クライアントモジュール WDK ネットワークモジュールレジストラー、登録
- 登録 (クライアントモジュールを)
- 初期化 (クライアントモジュールを)
- NmrRegisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d928d6e7b46c8364cc797a3040358dd65ed4cd40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824483"
---
# <a name="initializing-and-registering-a-client-module"></a>クライアント モジュールの初期化と登録


クライアントモジュールは、ネットワークモジュールレジストラー (NMR) に登録する前に、いくつかのデータ構造を初期化する必要があります。 これらの構造体には、 [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造体、 [**NPI\_クライアント\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)構造、 [**NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)構造 (NPI 内に含まれる) が含まれ\_クライアント\_特性の構造) と、クライアントモジュールの登録コンテキストに使用されるクライアントモジュールで定義されている構造体。

クライアントモジュールが NPI 固有のクライアント特性を定義する[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)のクライアントとして自身を NMR に登録する場合、クライアントモジュールは、で定義されているクライアント特性構造のインスタンスを初期化する必要もあります。NPI。

クライアントモジュールが NMR に登録されている限り、これらのデータ構造はすべて有効であり、メモリ内に常駐している必要があります。

たとえば、"EXNPI" NPI で、ヘッダーファイル Exnpi に次のものが定義されているとします。

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

次に、EXNPI NPI のクライアントとして登録するクライアントモジュールが、これらのすべてのデータ構造を初期化する方法を示します。

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

クライアントモジュールは通常、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内で自身を初期化します。 クライアントモジュールの主な初期化タスクは次のとおりです。

-   [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を指定します。 オペレーティングシステムは、クライアントモジュールがシステムからアンロードされるときに、この関数を呼び出します。 クライアントモジュールが unload 関数を提供しない場合、クライアントモジュールをシステムからアンロードすることはできません。

-   クライアントモジュールを NMR に登録するには、 [**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)関数を呼び出します。

次に、例を示します。

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

クライアントモジュールが複数の NPI のクライアントである場合は、独立したデータ構造のセットを初期化し、サポートする各 NPI に対して[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)を呼び出す必要があります。 ネットワークモジュールがクライアントモジュールとプロバイダーモジュールの両方 (つまり、1つの NPI のクライアントであり、別の NPI のプロバイダー) である場合、2つの独立したデータ構造セット (1 つはクライアントインターフェイス用、もう1つはプロバイダーインターフェイス用) を初期化する必要があります。を呼び出し、 **NmrRegisterClient**と[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)の両方を呼び出します。

クライアントモジュールは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内から[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)を呼び出す必要はありません。 たとえば、クライアントモジュールが複雑なドライバーのサブコンポーネントである場合、クライアントモジュールの登録は、クライアントモジュールサブコンポーネントがアクティブ化されている場合にのみ発生する可能性があります。

クライアントモジュールの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数の実装の詳細については、「[クライアントモジュールのアンロード](unloading-a-client-module.md)」を参照してください。

 

 





