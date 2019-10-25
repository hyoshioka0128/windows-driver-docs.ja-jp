---
title: クライアント モジュールへのプロバイダー モジュールのアタッチ
description: クライアント モジュールへのプロバイダー モジュールのアタッチ
ms.assetid: 5c68273e-d343-4d83-8703-957960934136
keywords:
- ネットワークモジュールの接続
- 登録 (ネットワークモジュールを)
- ネットワークモジュールレジストラー WDK、ネットワークモジュールの接続
- NMR WDK、アタッチ (ネットワークモジュールを)
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、アタッチ
- ネットワークモジュール WDK ネットワークモジュールレジストラー、添付ファイル
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09c7aaa8a31e0038ebcc780b84c81a71a3431a0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838224"
---
# <a name="attaching-a-provider-module-to-a-client-module"></a>クライアント モジュールへのプロバイダー モジュールのアタッチ


クライアントモジュールは、 [**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)関数を呼び出して、プロバイダーモジュールにそれ自体をアタッチします。 クライアントモジュールをプロバイダーモジュールにアタッチする方法の詳細については、「[プロバイダーモジュールへのクライアントモジュールのアタッチ](attaching-a-client-module-to-a-provider-module.md)」を参照してください。

クライアントモジュールが[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)を呼び出すと、NMR はプロバイダーモジュールの[*providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数を呼び出します。 NMR は、プロバイダーモジュールの*Providerattachclient*コールバック関数を呼び出すと、 *clientregistrationinstance*パラメーターに、関連付けられている[**NPI\_REGISTRATION\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)構造へのポインターを渡します。クライアントモジュールで**NmrClientAttachProvider**を呼び出します。 プロバイダーモジュールの*Providerattachclient*コールバック関数は、クライアントモジュールの**NPI\_登録\_インスタンス**構造のデータ、MODULEID 構造体とネットワークの[ **\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))データを使用できます。 [プログラミングインターフェイス (NPI)](network-programming-interface.md)固有のクライアント特性構造によってポイントされている**ModuleId**と**npiNPI の特性**のメンバーは、クライアントモジュールの **\_登録\_インスタンス**クライアントモジュールにアタッチするかどうかを決定する構造体。

プロバイダーモジュールによってクライアントモジュールにアタッチされることが判断された場合、プロバイダーモジュールの[*Providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数は次の操作を行う必要があります。

-   クライアントモジュールに、添付ファイルのバインディングコンテキスト構造を割り当てて初期化します。

-   *NmrBindingHandle*パラメーターで渡されたバインドハンドルを保存します。

-   プロバイダーモジュールがクライアントモジュールの NPI コールバック関数を呼び出すことができるように、 *ClientBindingContext*パラメーターと*clientdispatch*パラメーターに渡されたポインターを保存します。

-   *ProviderBindingContext*パラメーターが指す変数を、プロバイダーモジュールのバインディングコンテキスト構造を指すように設定します。

-   プロバイダーモジュールの NPI functions のディスパッチテーブルを含む構造体を指すように、 *Providerdispatch*パラメーターが指す変数を設定します。

-   STATUS\_SUCCESS に戻ります。

プロバイダーモジュールは通常、バインドハンドル、クライアントバインドコンテキストへのポインター、クライアントモジュールへのアタッチのバインドコンテキストにおけるクライアントディスパッチ構造へのポインターを保存します。

プロバイダーモジュールの[*Providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数が STATUS\_SUCCESS を返した場合、クライアントモジュールとプロバイダーモジュールは相互に正常にアタッチされています。

プロバイダーモジュールがクライアントモジュールにアタッチされないと判断した場合、プロバイダーモジュールの[*Providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数はステータス\_nointerface を返す必要があります。

たとえば、"EXNPI" ネットワークプログラミングインターフェイス (NPI) で、ヘッダーファイル Exnpi に次のものが定義されているとします。

```C++
// EXNPI client characteristics structure
typedef struct EXNPI_CLIENT_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_CLIENT_CHARACTERISTICS, *PEXNPI_CLIENT_CHARACTERISTICS;

// EXNPI client dispatch table
typedef struct EXNPI_CLIENT_DISPATCH_ {
  .
  . // NPI-specific dispatch table of function pointers that
  . // point to a client module's NPI callback functions.
  .
} EXNPI_CLIENT_DISPATCH, *PEXNPI_CLIENT_DISPATCH;

// EXNPI provider dispatch table
typedef struct EXNPI_PROVIDER_DISPATCH_ {
  .
  . // NPI-specific dispatch table of function pointers that
  . // point to a provider module's NPI functions.
  .
} EXNPI_PROVIDER_DISPATCH, *PEXNPI_PROVIDER_DISPATCH;
```

次のコード例は、EXNPI NPI のプロバイダーとして登録されているプロバイダーモジュールを、EXNPI NPI のクライアントとして登録されているクライアントモジュールにアタッチする方法を示しています。

```C++
// Context structure for the provider
// module's binding to a client module
typedef struct PROVIDER_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PVOID ClientBindingContext;
  PEXNPI_CLIENT_DISPATCH ClientDispatch;
  .
  . // Other provider-specific members
  .
} PROVIDER_BINDING_CONTEXT, *PPROVIDER_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// Structure for the provider's dispatch table
const EXNPI_PROVIDER_DISPATCH Dispatch = {
  .
  . // Function pointers to the provider
  . // module's NPI functions
  .
};

// ProviderAttachClient callback function
NTSTATUS
  ProviderAttachClient(
    IN HANDLE NmrBindingHandle,
    IN PVOID ProviderContext,
    IN PNPI_REGISTRATION_INSTANCE ClientRegistrationInstance,
    IN PVOID ClientBindingContext,
    IN CONST VOID *ClientDispatch,
    OUT PVOID *ProviderBindingContext,
    OUT PVOID *ProviderDispatch
    )
{
  PNPI_MODULEID ClientModuleId;
  PEXNPI_CLIENT_CHARACTERISTICS ClientNpiSpecificCharacteristics;
  PPROVIDER_BINDING_CONTEXT BindingContext;
  PVOID ClientBindingContext;
  PEXNPI_CLIENT_DISPATCH ClientDispatch;

  // Check parameters
  if ((ProviderBindingContext == NULL) ||
      (ProviderDispatch == NULL))
  {
    // Return error status code
    return STATUS_INVALID_PARAMETER;
  }

  // Get pointers to the client module's identification structure
  // and the client module's NPI-specific characteristics structure
  ClientModuleId = ClientRegistrationInstance->ModuleId;
  ClientNpiSpecificCharacteristics =
    (PEXNPI_CLIENT_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // Use the data in the structures pointed to by
  // ClientRegistrationInstance, ClientModuleId,
  // and ClientNpiSpecificCharacteristics to determine
  // whether to attach to the client module.
  //

  // If the provider module determines that it will not attach
  // to the client module
  if (...)
  {
    // Return status code indicating the modules did not
    // attach to each other
    return STATUS_NOINTERFACE;
  }

  // Allocate memory for the provider module's
  // binding context structure
  BindingContext =
    (PPROVIDER_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(PROVIDER_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the provider binding context structure
  ...

  // Save NmrBindingHandle, ClientBindingContext,
  // and ClientDispatch for future reference
  BindingContext->NmrBindingHandle =
    NmrBindingHandle;
  BindingContext->ClientBindingContext =
    ClientBindingContext;
  BindingContext->ClientDispatch =
    ClientDispatch;

  // Return a pointer to the provider binding context structure
  // in the ProviderBindingContext parameter
  *ProviderBindingContext = BindingContext;

  // Return a pointer to the provider dispatch structure
  // in the ProviderDispatch parameter
  *ProviderDispatch = &Dispatch;

  // Return success status
  return STATUS_SUCCESS;
}
```

 

 





