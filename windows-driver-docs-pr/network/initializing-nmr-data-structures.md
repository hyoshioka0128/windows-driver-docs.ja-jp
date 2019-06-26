---
title: NMR データ構造の初期化
description: NMR データ構造の初期化
ms.assetid: 84241ff4-f6ae-4c71-a9e3-1a6615e41293
keywords:
- ネットワーク モジュール レジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
- NMR データ構造体の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a13d3526117e3ffaca5cb0f334d678a00000e9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381259"
---
# <a name="initializing-nmr-data-structures"></a>NMR データ構造の初期化


Winsock カーネル (WSK) する前にアプリケーションに登録することができます、[ネットワーク モジュール レジストラー (NMR)](network-module-registrar2.md)、最初、アプリケーションは、次の構造を初期化する可能性があります。

-   [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))

-   [**NPI\_クライアント\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_client_characteristics)

-   [**NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance)内に含まれる、 [ **NPI\_クライアント\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_client_characteristics)構造体

有効であり、メモリに常駐のまま、NMR で WSK アプリケーションが登録されている限り、これらのデータ構造のすべて必要があります。

次のコード例では、WSK アプリケーションが初期化前の表に、データ構造のすべての方法を示します。

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

WSK アプリケーションが呼び出す、 [ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient) NMR にアプリケーションを登録する関数。

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

WSK アプリケーションを呼び出す必要はありません**NmrRegisterClient**内からその**DriverEntry**関数。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントの場合は、WSK アプリケーションのサブコンポーネントがアクティブな場合にのみが、アプリケーションの登録することがあります。

 

 





