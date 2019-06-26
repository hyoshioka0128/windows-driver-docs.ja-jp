---
title: クライアント モジュールへのプロバイダー モジュールのアタッチ
description: クライアント モジュールへのプロバイダー モジュールのアタッチ
ms.assetid: 5c68273e-d343-4d83-8703-957960934136
keywords:
- ネットワーク モジュールのアタッチ
- ネットワーク モジュールの登録
- ネットワーク モジュール レジストラー WDK は、ネットワーク モジュールのアタッチ
- ネットワーク モジュールのアタッチ、NMR WDK
- プロバイダー モジュール アタッチ WDK ネットワーク モジュール レジストラー
- ネットワーク モジュール WDK ネットワーク モジュールの登録、添付ファイル
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b86d68fbdd57f01a859393c07d96efad1aa1f798
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384421"
---
# <a name="attaching-a-provider-module-to-a-client-module"></a>クライアント モジュールへのプロバイダー モジュールのアタッチ


クライアント モジュールを呼び出す、 [ **NmrClientAttachProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)プロバイダー モジュールに接続する関数。 クライアント モジュールをプロバイダー モジュールに接続する方法の詳細については、次を参照してください。[プロバイダー モジュールへのクライアント モジュール](attaching-a-client-module-to-a-provider-module.md)します。

クライアント モジュールを呼び出すと[ **NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)、NMR 呼び出し、プロバイダー モジュールの[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数。 NMR がプロバイダーのモジュールを呼び出したときに*ProviderAttachClient*コールバック関数では、合格したで、 *ClientRegistrationInstance*パラメーターへのポインター、 [ **NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance)を呼び出したクライアント モジュールに関連付けられている構造**NmrClientAttachProvider**します。 プロバイダー モジュールの*ProviderAttachClient*コールバック関数は、データを使用して、クライアントのモジュールで**NPI\_登録\_インスタンス**データを構成します。[**NPI\_MODULEID** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))構造と[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)-特定のクライアントの特性構造が、が指す**ModuleId**と**NpiSpecificCharacteristics**クライアントのモジュールのメンバー **NPI\_登録\_インスタンス**構造体かどうかは、クライアント モジュールに接続を確認します。

プロバイダーのモジュール プロバイダー モジュールのクライアントのモジュールを接続すると判断した場合[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数は、次を実行する必要があります。

-   割り当ておよびクライアント モジュールに添付ファイルのバインド コンテキストの構造体を初期化します。

-   渡されたバインド ハンドルを保存、 *NmrBindingHandle*パラメーター。

-   渡されたポインターを保存、 *ClientBindingContext*と*ClientDispatch*パラメーター プロバイダー モジュールは、クライアントのモジュールの NPI コールバック関数への呼び出しを行うことができるようにします。

-   指す変数を設定、 *ProviderBindingContext*プロバイダー モジュールをポイントするパラメーターの context 構造にバインドします。

-   指す変数を設定、 *ProviderDispatch* NPI 関数のプロバイダー モジュールのディスパッチ テーブルを格納する構造体をポイントするパラメーター。

-   状態を返す\_成功します。

プロバイダー モジュールでは、クライアント モジュールに添付ファイルのバインド コンテキストのクライアント ディスパッチ構造に、バインド ハンドル、クライアントのバインド コンテキストへのポインターとポインターが通常保存します。

プロバイダー モジュールの場合、 [ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数が返すステータス\_成功した場合、クライアントのモジュールおよびプロバイダー モジュールが正常に相互に接続されています。

プロバイダー モジュールを決定し、クライアントのモジュール、プロバイダー モジュールのアタッチがない場合[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数は、状態を返す必要があります\_NOINTERFACE します。

たとえば、"EXNPI"ネットワーク プログラミング インターフェイス (NPI) Exnpi.h のヘッダー ファイルで、次を定義します。

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

次のコード例では、どのように EXNPI NPI のプロバイダーとして登録されているプロバイダー モジュールに接続できる EXNPI NPI のクライアントとして登録されているクライアント モジュールには示しています。

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

 

 





