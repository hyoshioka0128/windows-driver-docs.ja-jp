---
title: クライアント モジュールのプロバイダー モジュールへのアタッチ
description: クライアント モジュールのプロバイダー モジュールへのアタッチ
ms.assetid: 351c07f6-186a-4f47-95f8-c94084ff68fb
keywords:
- ネットワーク モジュールのアタッチ
- ネットワーク モジュールの登録
- ネットワーク モジュール レジストラー WDK は、ネットワーク モジュールのアタッチ
- ネットワーク モジュールのアタッチ、NMR WDK
- クライアントのモジュールのアタッチ、WDK ネットワーク モジュール レジストラー
- ネットワーク モジュール WDK ネットワーク モジュールの登録、添付ファイル
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd60a45c908fc4b59ad854fb5ad530743e5396b
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349891"
---
# <a name="attaching-a-client-module-to-a-provider-module"></a>クライアント モジュールのプロバイダー モジュールへのアタッチ


クライアント モジュールが登録されるとネットワーク モジュール レジストラー (NMR) で、NMR 呼び出してクライアント モジュールの[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)であるプロバイダー モジュールごとに 1 回のコールバック関数同じのプロバイダーとして登録されている[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)クライアント モジュールは、クライアントとして登録します。

クライアント モジュールの呼び出しも、NMR [ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)クライアント モジュールは、クライアントとして登録されている同じ NPI のプロバイダーとして、新しいプロバイダー モジュールを登録するたびに、コールバック関数.

NMR がクライアントのモジュールを呼び出したときに[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数の特定のプロバイダー モジュールでは、合格したで、 *ProviderRegistrationInstance*パラメーターへのポインター、 [ **NPI\_登録\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff568815)プロバイダー モジュールに関連付けられている構造体。 クライアント モジュールの*ClientAttachProvider*コールバック関数は、データを使用して、プロバイダー モジュールの**NPI\_登録\_インスタンス**内のデータと構造体[ **NPI\_MODULEID** ](https://msdn.microsoft.com/library/windows/hardware/ff568813)構造と NPI に固有のプロバイダーの特性構造が指す、 **ModuleId**と**NpiSpecificCharacteristics**のプロバイダー モジュールのメンバー **NPI\_登録\_インスタンス**構造体のかどうかは、プロバイダー モジュールに接続を確認します。

クライアント モジュールは、プロバイダー モジュールに、クライアントのモジュールの接続はそのことを決定します場合[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数は、のバインド コンテキストの構造体を初期化します。添付ファイルをプロバイダー モジュールとし、呼び出し、 [ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)添付ファイルの処理を続行する関数。 このような状況で、クライアントのモジュールの*ClientAttachProvider*コールバック関数によって返されるステータス コードを返す必要があります、 **NmrClientAttachProvider**関数。

場合[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)ステータスを返します\_成功した場合、クライアントのモジュールおよびプロバイダー モジュールが正常に相互に接続されています。 このような状況で、クライアントのモジュールの[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数に渡された、NMR バインド ハンドルを保存する必要があります、 *NmrBindingHandle*パラメーター、NMR には、クライアントのモジュールが呼び出されると*ClientAttachProvider*コールバック関数。 クライアント モジュールの*ClientAttachProvider*コールバック関数は、プロバイダーのバインド コンテキストとクライアント モジュールが、に渡される変数で返されるプロバイダーディスパッチテーブルに、ポインターを保存もする必要があります**NmrClientAttachProvider**で機能、 *ProviderBindingContext*と*ProviderDispatch*パラメーター。 通常、クライアント モジュールは、プロバイダー モジュールに添付ファイルのバインド コンテキストのこのデータを保存します。

場合[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)状態を返さない\_成功すると、クライアントのモジュールの[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数のクリーンアップおよびと呼ばれる前に、割り当てられたリソースを解放する必要があります**NmrClientAttachProvider**します。

クライアント モジュールを決定し、プロバイダー、モジュール、クライアント モジュールのアタッチがない場合[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数は、状態を返す必要があります\_NOINTERFACE します。

たとえば、"EXNPI"ネットワーク プログラミング インターフェイス (NPI) Exnpi.h のヘッダー ファイルで、次を定義します。

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

次のコード例では、どのように EXNPI NPI のクライアントとして登録されているクライアント モジュールに接続できる EXNPI NPI のプロバイダーとして登録されているプロバイダー モジュールには示しています。

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

 

 





