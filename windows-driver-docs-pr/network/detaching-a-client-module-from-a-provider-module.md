---
title: プロバイダー モジュールからのクライアント モジュールのデタッチ
description: プロバイダー モジュールからのクライアント モジュールのデタッチ
ms.assetid: 148c1a90-0fef-4b22-bf7e-f35285f1bc55
keywords:
- クライアント モジュール デタッチ WDK ネットワーク モジュール レジストラー
- NmrDeregisterClient
- ネットワーク モジュール WDK ネットワーク モジュールの登録、デタッチできません。
- ネットワーク モジュールの登録を解除
- ネットワーク モジュールをデタッチするネットワーク モジュールのレジストラー WDK
- ネットワーク モジュールのデタッチ、NMR WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daff59c87b971336033abe03c47b09dfca84f691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374884"
---
# <a name="detaching-a-client-module-from-a-provider-module"></a>プロバイダー モジュールからのクライアント モジュールのデタッチ


ときにクライアント モジュールの登録を解除ネットワーク モジュール レジストラー (NMR) を呼び出すことによって、 [ **NmrDeregisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterclient)関数の場合、NMR を呼び出すクライアント モジュールの[ *ClientDetachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_detach_provider_fn)それがアタッチされている、クライアントのモジュールでデタッチ自体からすべてのモジュール プロバイダー クライアント モジュールのパーツ 's プロセス登録の解除できるように各プロバイダー モジュールに対して 1 回のコールバック関数.

さらに、プロバイダー モジュールをされるたびにクライアント モジュールが接続されている登録を解除、NMR で呼び出すことによって、 [ **NmrDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterprovider)関数の場合、NMR もクライアント モジュールの呼び出し[*ClientDetachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_detach_provider_fn)コールバック関数クライアント モジュールからデタッチできます自体プロバイダー モジュール プロバイダー モジュールのパーツ 's プロセス登録の解除できるようにします。

後にその[ *ClientDetachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_detach_provider_fn)コールバック関数が呼び出された、呼び出しのプロバイダー モジュールのいずれかにする必要がありますいないことをクライアント モジュール[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)関数。 プロバイダー モジュールの NPI 関数のいずれかに進行中の呼び出しがない場合とクライアント モジュールの*ClientDetachProvider*コールバック関数が呼び出されると、次に、 *ClientDetachProvider*コールバック関数は、状態を返す必要があります\_成功します。

モジュールの NPI 関数、プロバイダーの 1 つ以上の実行中の呼び出しがある場合とクライアント モジュールの[ *ClientDetachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_detach_provider_fn)コールバック関数が呼び出されると、次に、 *ClientDetachProvider*コールバック関数は、状態を返す必要があります\_保留します。 この場合、クライアント モジュールを呼び出す必要があります、 [ **NmrClientDetachProviderComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)プロバイダー モジュールの NPI 関数へのすべての実行中の呼び出しが完了した後も機能します。 呼び出し**NmrClientDetachProviderComplete** NMR クライアント モジュール プロバイダー モジュールからのデタッチが完了したことを通知します。

プロバイダー モジュールの NPI 関数の実行中の呼び出しの数を追跡する方法の詳細については、次を参照してください。[プログラミングに関する考慮事項](programming-considerations.md)します。

クライアント モジュールを実装する場合、 [ *ClientCleanupBindingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)コールバック関数、NMR を呼び出すクライアント モジュールの*ClientCleanupBindingContext*コールバッククライアントのモジュールとプロバイダー、モジュールの両方には、互いからのデタッチを完了した後の関数。 クライアント モジュールの*ClientCleanupBindingContext*コールバック関数は、クライアント モジュールのバインド コンテキストの構造体に含まれるデータのために必要なクリーンアップを実行する必要があります。 バインド コンテキストの構造体のメモリは、クライアント モジュールは、構造のメモリを動的に割り当てられる場合そのに解放する必要があります。

以下に例を示します。

```C++
// ClientDetachProvider callback function
NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    )
{
  PCLIENT_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PCLIENT_BINDING_CONTEXT)ClientBindingContext;

  // Set a flag indicating that the client module is detaching
  // from the provider module so that no more calls are made to
  // the provider module's NPI functions.
  ...

  // Check if there are no in-progress NPI function calls to the
  // provider module
  if (...)
  {
    // Return success status indicating detachment is complete
    return STATUS_SUCCESS;
  }

  // There are one or more in-progress NPI function calls
  // to the provider module
  else
  {
    // Return pending status indicating detachment is pending
    // completion of the in-progress NPI function calls
    return STATUS_PENDING;

    // When the last in-progress call to the provider module's
    // NPI functions completes, the client module must call
    // NmrClientDetachProviderComplete() with the binding handle
    // for the attachment to the provider module.
  }
}

// ClientCleanupBindingContext callback function
VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    )
{
  PCLIENT_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PCLIENT_BINDING_CONTEXT)ClientBindingContext;

  // Clean up the client binding context structure
  ...

  // Free the memory for client's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

 

 





