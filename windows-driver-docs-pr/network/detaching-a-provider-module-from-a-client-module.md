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
ms.openlocfilehash: 6852d48f426a1c09c124eb1d510dc694e9ef3a51
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350425"
---
# <a name="detaching-a-provider-module-from-a-client-module"></a>クライアント モジュールからのプロバイダー モジュールのデタッチ


ときにプロバイダー モジュールの登録を解除ネットワーク モジュール レジストラー (NMR) を呼び出すことによって、 [ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)関数の場合、NMR 呼び出し、プロバイダー モジュールの[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)それがアタッチされている、プロバイダー モジュールでデタッチ自体からすべてのクライアントのモジュール プロバイダー モジュールのパーツ 's プロセス登録の解除できるようにクライアント モジュールごとに 1 回のコールバック関数.

さらに、クライアント モジュールをされるたびに、プロバイダー モジュールが接続されている登録を解除します、NMR で呼び出すことによって、 [ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)関数の場合、NMR もプロバイダー モジュールの呼び出し[*ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)コールバック関数、プロバイダー モジュールからデタッチできます自体クライアント モジュール クライアント モジュールのパーツ 's プロセス登録の解除できるようにします。

後にその[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)コールバック関数が呼び出された、呼び出しのクライアント モジュールのいずれかにする必要がありますいないことをプロバイダー モジュール[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)コールバック関数。 クライアント モジュールの NPI コールバック関数のいずれかに進行中の呼び出しがない場合と、プロバイダー モジュールの*ProviderDetachClient*コールバック関数が呼び出されると、次に、 *ProviderDetachClient*コールバック関数は、状態を返す必要があります\_成功します。

モジュールの NPI コールバック関数を 1 つ以上のクライアントの進行中の呼び出しがある場合と、プロバイダー モジュールの[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)コールバック関数が呼び出された、 *ProviderDetachClient*コールバック関数は、状態を返す必要があります\_保留します。 この場合、プロバイダー モジュールを呼び出す必要があります、 [ **NmrProviderDetachClientComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568781)クライアント モジュールの NPI コールバック関数へのすべての実行中の呼び出しが完了した後も機能します。 呼び出し**NmrProviderDetachClientComplete** NMR プロバイダー モジュール クライアント モジュールからのデタッチが完了したことを通知します。

クライアント モジュールの NPI コールバック関数の実行中の呼び出しの数を追跡する方法の詳細については、[プログラミングに関する考慮事項](programming-considerations.md)を参照してください。

プロバイダーのモジュールを実装する場合、 [ *ProviderCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff570396)コールバック関数、NMR 呼び出し、プロバイダー モジュールの*ProviderCleanupBindingContext*プロバイダー モジュールおよびクライアント モジュールの両方がお互いからのデタッチを完了してからのコールバック関数。 プロバイダー モジュールの*ProviderCleanupBindingContext*コールバック関数は、プロバイダー モジュールのバインド コンテキストの構造体に含まれるデータのために必要なクリーンアップを実行する必要があります。 バインド コンテキストの構造体のメモリは、プロバイダー モジュールは、構造のメモリを動的に割り当てられる場合そのに解放する必要があります。

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

 

 





