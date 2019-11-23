---
title: クライアント モジュールからのプロバイダー モジュールのデタッチ
description: クライアント モジュールからのプロバイダー モジュールのデタッチ
ms.assetid: 011d0770-6942-480e-95ee-88a2903822b2
keywords:
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、デタッチ
- ネットワークモジュール WDK ネットワークモジュールレジストラー、デタッチ
- ネットワークモジュールの登録解除
- ネットワークモジュールレジストラー WDK、ネットワークモジュールのデタッチ
- NMR WDK、デタッチ (ネットワークモジュールを)
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87f6c6065bb14a8ecca4786425f2f5785da65e08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838152"
---
# <a name="detaching-a-provider-module-from-a-client-module"></a>クライアント モジュールからのプロバイダー モジュールのデタッチ


プロバイダーモジュールが[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)関数を呼び出すことによってネットワークモジュールレジストラー (NMR) と解除すると、NMR はプロバイダーモジュールの[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) callback 関数を呼び出します。各クライアントモジュールに対して、プロバイダーモジュールの登録解除プロセスの一部として、すべてのクライアントモジュールからプロバイダーモジュールをデタッチできるように、アタッチされます。

さらに、プロバイダーモジュールがアタッチされているクライアントモジュールが[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)関数を呼び出して NMR に解除するたびに、NMR はプロバイダーモジュールの[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) callback 関数も呼び出します。プロバイダーモジュールは、クライアントモジュールの登録解除プロセスの一部として、クライアントモジュールから自身をデタッチできます。

[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) callback 関数が呼び出された後、プロバイダーモジュールは、クライアントモジュールの[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)コールバック関数に対してそれ以上の呼び出しを行うことはできません。 プロバイダーモジュールの*ProviderDetachClient* callback 関数が呼び出されたときに、クライアントモジュールの NPI コールバック関数のいずれかに対して実行中の呼び出しがない場合は、 *ProviderDetachClient* callback 関数から STATUS\_SUCCESS が返されます。

プロバイダーモジュールの[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) callback 関数が呼び出されたときに、クライアントモジュールの NPI コールバック関数の1つ以上の呼び出しが進行中の場合、 *ProviderDetachClient* callback 関数は状態を返す必要があります。\_保留中です。 この場合、プロバイダーモジュールは、クライアントモジュールの NPI コールバック関数の実行中のすべての呼び出しが完了した後に、 [**NmrProviderDetachClientComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrproviderdetachclientcomplete)関数を呼び出す必要があります。 **NmrProviderDetachClientComplete**を呼び出すと、クライアントモジュールからのプロバイダーモジュールのデタッチが完了したことが NMR に通知されます。

クライアントモジュールの NPI コールバック関数に対する実行中の呼び出しの数を追跡する方法の詳細については、「[プログラミングの考慮事項](programming-considerations.md)」を参照してください。

プロバイダーモジュールが[*ProviderCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_cleanup_binding_context_fn)コールバック関数を実装している場合、プロバイダーモジュールとクライアントモジュールの両方が完了した後、NMR はプロバイダーモジュールの*ProviderCleanupBindingContext*コールバック関数を呼び出します。相互にデタッチ。 プロバイダーモジュールの*ProviderCleanupBindingContext* callback 関数は、プロバイダーモジュールのバインディングコンテキスト構造内に含まれるデータの必要なクリーンアップを実行する必要があります。 その後、プロバイダーモジュールが構造体のメモリを動的に割り当てた場合、バインドコンテキストの構造に対してメモリを解放する必要があります。

次に、例を示します。

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

 

 





