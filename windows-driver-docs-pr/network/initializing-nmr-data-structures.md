---
title: NMR データ構造の初期化
description: NMR データ構造の初期化
ms.assetid: 84241ff4-f6ae-4c71-a9e3-1a6615e41293
keywords:
- ネットワークモジュールレジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
- NMR データ構造体の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c58da13ba5823fe2dcb55ad41cc0dbbb83b55fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824415"
---
# <a name="initializing-nmr-data-structures"></a>NMR データ構造の初期化


Winsock カーネル (WSK) アプリケーションを[ネットワークモジュールレジストラー (NMR)](network-module-registrar2.md)に登録するには、まず、アプリケーションで次の構造を初期化する必要があります。

-   [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))

-   [**NPI\_クライアント\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)

-   [**NPI\_クライアントの\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)の構造に含まれる[ **\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)

WSK アプリケーションが NMR に登録されている限り、これらのデータ構造はすべて有効であり、メモリ内に常駐している必要があります。

次のコード例は、WSK アプリケーションで、前に示したすべてのデータ構造を初期化する方法を示しています。

```C++
// Include the WSK header file
#include "wsk.h"

// Structure for the WSK application's network module identification
const NPI_MODULEID ModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the WSK application
};

// Prototypes for the WSK application's NMR API callback functions
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

// Structure for the WSK application's characteristics
const NPI_CLIENT_CHARACTERISTICS Characteristics =
{
  0,
  sizeof(NPI_CLIENT_CHARACTERISTICS),
  ClientAttachProvider,
  ClientDetachProvider,
  ClientCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &NPI_WSK_INTERFACE_ID,
    &ModuleId,
    0,
    NULL
  }
};
```

WSK アプリケーションは、 [**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)関数を呼び出して、NMR にアプリケーションを登録します。

次に、例を示します。

```C++
// Variable to contain the handle for the registration with the NMR
HANDLE RegistrationHandle;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;

  .
  .
  .

  // Register the WSK application with the NMR
  Status = NmrRegisterClient(
    &Characteristics,
    NULL,
    &RegistrationHandle
    );

  if(!NT_SUCCESS(Status)) {
      .
      .
      .
      return Status;
  }

  .
  .
  .
}
```

WSK アプリケーションは、 **Driverentry**関数内から**NmrRegisterClient**を呼び出す必要はありません。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントである場合、WSK アプリケーションサブコンポーネントがアクティブになっている場合にのみ、アプリケーションの登録が発生する可能性があります。

 

 





