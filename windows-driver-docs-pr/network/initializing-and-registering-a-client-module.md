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
ms.openlocfilehash: 01e7d2f1eb0ea343c27eef4d0d897bc2155d9037
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324945"
---
# <a name="initializing-and-registering-a-client-module"></a>クライアント モジュールの初期化と登録


クライアント モジュールは、ネットワーク モジュール レジストラー (NMR) で登録にする前に、さまざまなデータ構造体を初期化する必要があります。 これらの構造が含まれます、 [ **NPI\_MODULEID** ](https://msdn.microsoft.com/library/windows/hardware/ff568813)構造、 [ **NPI\_クライアント\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff568812)構造、 [ **NPI\_登録\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff568815)構造 (、NPI 内に含まれる\_クライアント\_の特性構造)、およびクライアント モジュールの登録のコンテキストに使用されるクライアント モジュールで定義された構造です。

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

クライアントのモジュールが通常初期化自体内でその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 モジュールのクライアントのメインの初期化タスクは次のとおりです。

-   指定、 [**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 オペレーティング システムは、クライアント モジュールがシステムからアンロードされるときに、この関数を呼び出します。 クライアント モジュールはアンロード、関数を提供していない場合、クライアント モジュールは、システムからアンロードすることはできません。

-   呼び出す、 [ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782) NMR をクライアント モジュールを登録する関数。

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

データ構造と呼び出しの独立したセットを初期化する必要がありますクライアント モジュールが 1 つ以上の NPI のクライアントの場合は、 [ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)各 NPI でサポートされるのです。 ネットワーク モジュールがクライアント モジュールとプロバイダー モジュールの両方のかどうか (つまり、NPI の 1 つのクライアントおよび別の NPI のプロバイダー) である 2 つの独立したデータ構造、クライアント インターフェイスおよびプロバイダー インターフェイスのセットを初期化する必要があります、両方を呼び出すと**NmrRegisterClient**と[ **NmrRegisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff568784)します。

クライアント モジュールを呼び出す必要はありません[ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)内からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 たとえば、クライアント モジュールが複雑なドライバーのサブコンポーネントが場合、クライアント モジュールの登録が発生するクライアントのサブコンポーネントのモジュールがアクティブな場合にのみ。

クライアント モジュールの実装の詳細については[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数を参照してください[クライアント モジュールをアンロード](unloading-a-client-module.md)します。

 

 





