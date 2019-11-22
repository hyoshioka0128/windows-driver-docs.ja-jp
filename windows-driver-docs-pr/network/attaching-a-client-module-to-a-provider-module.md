---
title: クライアント モジュールのプロバイダー モジュールへのアタッチ
description: クライアント モジュールのプロバイダー モジュールへのアタッチ
ms.assetid: 351c07f6-186a-4f47-95f8-c94084ff68fb
keywords:
- ネットワークモジュールの接続
- 登録 (ネットワークモジュールを)
- ネットワークモジュールレジストラー WDK、ネットワークモジュールの接続
- NMR WDK、アタッチ (ネットワークモジュールを)
- クライアントモジュール WDK ネットワークモジュールレジストラー、アタッチ
- ネットワークモジュール WDK ネットワークモジュールレジストラー、添付ファイル
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80289c05dce52ae84dc6ca572622286231481e43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838229"
---
# <a name="attaching-a-client-module-to-a-provider-module"></a>クライアント モジュールのプロバイダー モジュールへのアタッチ


クライアントモジュールがネットワークモジュールレジストラー (NMR) に登録されると、クライアントモジュールがクライアントとして登録したのと同じ[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)のプロバイダーとして登録されているプロバイダーモジュールごとに、NMR によってクライアントモジュールの[*clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数が呼び出されます。

また、NMR は、クライアントモジュールがクライアントとして登録したものと同じ NPI のプロバイダーとして新しいプロバイダーモジュールが登録されるたびに、クライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数を呼び出します。

NMR が、特定のプロバイダーモジュールに対してクライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数を呼び出すと、 *providerregistrationinstance*パラメーターに、 [**NPI\_REGISTRATION\_インスタンスへのポインターを渡します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)プロバイダーモジュールに関連付けられている構造体。 クライアントモジュールの*Clientattachprovider*コールバック関数は、プロバイダーモジュールの**NPI\_登録\_インスタンス**構造のデータだけでなく、 [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造体のデータと、プロバイダーモジュールの**NPI\_登録\_インスタンス**構造によってポイントさ**れている**NPI 固有のプロバイダー**特性の構造**は、それが必要かどうかを判断します。プロバイダーモジュールにアタッチします。

クライアントモジュールによってプロバイダーモジュールにアタッチされることが判断された場合、クライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数は、プロバイダーモジュールへの添付ファイルのバインドコンテキスト構造を割り当てて初期化し、[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)関数は、添付ファイルの処理を続行します。 この場合、クライアントモジュールの*Clientattachprovider*コールバック関数は、 **NmrClientAttachProvider**関数によって返されたステータスコードを返す必要があります。

[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)が STATUS\_SUCCESS を返した場合、クライアントモジュールとプロバイダモジュールが相互に正常にアタッチされています。 この場合、クライアントモジュールの[*clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数は、NMR がクライアントモジュールの*clientattachprovider*を呼び出したときに、NMR が*NmrBindingHandle*パラメーターに渡したバインドハンドルを保存する必要があります。コールバック関数。 クライアントモジュールの*Clientattachprovider*コールバック関数は、プロバイダーバインドコンテキストへのポインターと、クライアントモジュールによって**NmrClientAttachProvider**関数に渡された変数に返されるプロバイダーディスパッチテーブルも、 *ProviderBindingContext*および*providerdispatch*パラメーターに保存する必要があります。 クライアントモジュールは、通常、プロバイダーモジュールへの添付ファイルのバインドコンテキストにこのデータを保存します。

[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)が正常に状態\_返さない場合、クライアントモジュールの[*clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数は、 **NmrClientAttachProvider**という名前の前に割り当てられたすべてのリソースをクリーンアップして解放する必要があります.

クライアントモジュールがプロバイダーモジュールにアタッチされないと判断した場合、クライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数はステータス\_nointerface を返す必要があります。

たとえば、"EXNPI" ネットワークプログラミングインターフェイス (NPI) で、ヘッダーファイル Exnpi に次のものが定義されているとします。

```C++
// EXNPI provider characteristics structure
typedef struct EXNPI_PROVIDER_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_PROVIDER_CHARACTERISTICS, *PEXNPI_PROVIDER_CHARACTERISTICS;

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

次のコード例は、EXNPI NPI のクライアントとして登録されているクライアントモジュールを、EXNPI NPI のプロバイダーとして登録されているプロバイダーモジュールにアタッチする方法を示しています。

```C++
// Context structure for the client
// module's binding to a provider module
typedef struct CLIENT_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  .
  . // Other client-specific members
  .
} CLIENT_BINDING_CONTEXT, *PCLIENT_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// Structure for the client's dispatch table
const EXNPI_CLIENT_DISPATCH Dispatch = {
  .
  . // Function pointers to the client module's
  . // NPI callback functions
  .
};

// ClientAttachProvider callback function
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    )
{
  PNPI_MODULEID ProviderModuleId;
  PEXNPI_PROVIDER_CHARACTERISTICS ProviderNpiSpecificCharacteristics;
  PCLIENT_BINDING_CONTEXT BindingContext;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  NTSTATUS Status;

  // Get pointers to the provider module's identification structure
  // and the provider module's NPI-specific characteristics structure
  ProviderModuleId = ProviderRegistrationInstance->ModuleId;
  ProviderNpiSpecificCharacteristics =
    (PEXNPI_PROVIDER_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // Use the data in the structures pointed to by
  // ProviderRegistrationInstance, ProviderModuleId,
  // and ProviderNpiSpecificCharacteristics to determine
  // whether to attach to the provider module.
  //

  // If the client module determines that it will not attach
  // to the provider module
  if (...)
  {
    // Return status code indicating the modules did not
    // attach to each other
    return STATUS_NOINTERFACE;
  }

  // Allocate memory for the client module's
  // binding context structure
  BindingContext =
    (PCLIENT_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(CLIENT_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the client binding context structure
  ...
 
  // Continue with the attachment to the provider module
  Status = NmrClientAttachProvider(
    NmrBindingHandle,
    BindingContext,
    &Dispatch,
    &ProviderBindingContext,
    &ProviderDispatch
    );

  // Check result of attachment
  if (Status == STATUS_SUCCESS)
  {
    // Save NmrBindingHandle, ProviderBindingContext,
    // and ProviderDispatch for future reference
    BindingContext->NmrBindingHandle =
      NmrBindingHandle;
    BindingContext->ProviderBindingContext =
      ProviderBindingContext;
    BindingContext->ProviderDispatch =
      ProviderDispatch;
  }

  // Attachment did not succeed
  else
  {
    // Free memory for client's binding context structure
    ExFreePoolWithTag(
      BindingContext,
      BINDING_CONTEXT_POOL_TAG
      );
  }

  // Return result of attachment
  return Status;
}
```

 

 





