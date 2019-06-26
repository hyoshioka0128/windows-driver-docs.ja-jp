---
title: クライアント モジュールからのプロバイダー モジュールのデタッチ
description: クライアント モジュールからのプロバイダー モジュールのデタッチ
ms.assetid: 011d0770-6942-480e-95ee-88a2903822b2
keywords:
- プロバイダー モジュール デタッチ WDK ネットワーク モジュール レジストラー
- ネットワーク モジュール WDK ネットワーク モジュールの登録、デタッチできません。
- ネットワーク モジュールの登録を解除
- ネットワーク モジュールをデタッチするネットワーク モジュールのレジストラー WDK
- ネットワーク モジュールのデタッチ、NMR WDK
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2ae1a5132676debf2375550470c8a339b0c14d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381430"
---
# <a name="detaching-a-provider-module-from-a-client-module"></a>クライアント モジュールからのプロバイダー モジュールのデタッチ


ときにプロバイダー モジュールの登録を解除ネットワーク モジュール レジストラー (NMR) を呼び出すことによって、 [ **NmrDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterprovider)関数の場合、NMR 呼び出し、プロバイダー モジュールの[ *ProviderDetachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_detach_client_fn)それがアタッチされている、プロバイダー モジュールでデタッチ自体からすべてのクライアントのモジュール プロバイダー モジュールのパーツ 's プロセス登録の解除できるようにクライアント モジュールごとに 1 回のコールバック関数.

さらに、クライアント モジュールをされるたびに、プロバイダー モジュールが接続されている登録を解除します、NMR で呼び出すことによって、 [ **NmrDeregisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterclient)関数の場合、NMR もプロバイダー モジュールの呼び出し[*ProviderDetachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_detach_client_fn)コールバック関数、プロバイダー モジュールからデタッチできます自体クライアント モジュール クライアント モジュールのパーツ 's プロセス登録の解除できるようにします。

後にその[ *ProviderDetachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_detach_client_fn)コールバック関数が呼び出された、呼び出しのクライアント モジュールのいずれかにする必要がありますいないことをプロバイダー モジュール[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)コールバック関数。 クライアント モジュールの NPI コールバック関数のいずれかに進行中の呼び出しがない場合と、プロバイダー モジュールの*ProviderDetachClient*コールバック関数が呼び出されると、次に、 *ProviderDetachClient*コールバック関数は、状態を返す必要があります\_成功します。

モジュールの NPI コールバック関数を 1 つ以上のクライアントの進行中の呼び出しがある場合と、プロバイダー モジュールの[ *ProviderDetachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_detach_client_fn)コールバック関数が呼び出された、 *ProviderDetachClient*コールバック関数は、状態を返す必要があります\_保留します。 この場合、プロバイダー モジュールを呼び出す必要があります、 [ **NmrProviderDetachClientComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrproviderdetachclientcomplete)クライアント モジュールの NPI コールバック関数へのすべての実行中の呼び出しが完了した後も機能します。 呼び出し**NmrProviderDetachClientComplete** NMR プロバイダー モジュール クライアント モジュールからのデタッチが完了したことを通知します。

クライアント モジュールの NPI コールバック関数の実行中の呼び出しの数を追跡する方法の詳細については、次を参照してください。[プログラミングに関する考慮事項](programming-considerations.md)します。

プロバイダーのモジュールを実装する場合、 [ *ProviderCleanupBindingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_cleanup_binding_context_fn)コールバック関数、NMR 呼び出し、プロバイダー モジュールの*ProviderCleanupBindingContext*プロバイダー モジュールおよびクライアント モジュールの両方がお互いからのデタッチを完了してからのコールバック関数。 プロバイダー モジュールの*ProviderCleanupBindingContext*コールバック関数は、プロバイダー モジュールのバインド コンテキストの構造体に含まれるデータのために必要なクリーンアップを実行する必要があります。 バインド コンテキストの構造体のメモリは、プロバイダー モジュールは、構造のメモリを動的に割り当てられる場合そのに解放する必要があります。

例:

```C++
// ProviderDetachClient callback function
NTSTATUS
  ProviderDetachClient(
    IN PVOID ProviderBindingContext
    )
{
  PPROVIDER_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PPROVIDER_BINDING_CONTEXT)ProviderBindingContext;

  // Set a flag indicating that the provider module is detaching
  // from the client module so that no more calls are made to
  // the client module's NPI callback functions.
  ...

  // Check if there are no in-progress NPI callback function calls
  // to the client module
  if (...)
  {
    // Return success status indicating detachment is complete
    return STATUS_SUCCESS;
  }

  // There are one or more in-progress NPI callback function
  // calls to the client module
  else
  {
    // Return pending status indicating detachment is pending
    // completion of the in-progress NPI callback function calls
    return STATUS_PENDING;

    // When the last in-progress call to the client module's
    // NPI callback functions completes, the provider module
    // must call NmrProviderDetachClientComplete() with the
    // binding handle for the attachment to the client module.
  }
}

// ProviderCleanupBindingContext callback function
VOID
  ProviderCleanupBindingContext(
    IN PVOID ProviderBindingContext
    )
{
  PPROVIDER_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PPROVIDER_BINDING_CONTEXT)ProviderBindingContext;

  // Clean up the provider binding context structure
  ...

  // Free the memory for provider's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

 

 





