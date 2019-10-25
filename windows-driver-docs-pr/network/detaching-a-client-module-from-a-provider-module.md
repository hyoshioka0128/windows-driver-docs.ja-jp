---
title: プロバイダーモジュールからクライアントモジュールをデタッチする
description: プロバイダーモジュールからクライアントモジュールをデタッチする
ms.assetid: 148c1a90-0fef-4b22-bf7e-f35285f1bc55
keywords:
- クライアントモジュール WDK ネットワークモジュールレジストラー, デタッチ
- NmrDeregisterClient
- ネットワークモジュール WDK ネットワークモジュールレジストラー、デタッチ
- ネットワークモジュールの登録解除
- ネットワークモジュールレジストラー WDK、ネットワークモジュールのデタッチ
- NMR WDK、デタッチ (ネットワークモジュールを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4c26fdda7a295f851c9dd23edb8e9cfea8dbc8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838155"
---
# <a name="detaching-a-client-module-from-a-provider-module"></a>プロバイダーモジュールからクライアントモジュールをデタッチする


クライアントモジュールが[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)関数を呼び出すことによってネットワークモジュールレジストラー (NMR) と解除した場合、NMR はクライアントモジュールの[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数を呼び出します。この関数は、プロバイダーモジュールごとに1回呼び出されます。クライアントモジュールの登録解除プロセスの一部として、すべてのプロバイダーモジュールからクライアントモジュールをデタッチできるように、アタッチされます。

さらに、 [**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)関数を呼び出すことにより、クライアントモジュールがアタッチされているプロバイダーモジュールが NMR に解除するたびに、NMR はクライアントモジュールの[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数も呼び出します。クライアントモジュールは、プロバイダーモジュールの登録解除プロセスの一部として、プロバイダーモジュールから自身をデタッチできます。

[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数が呼び出された後、クライアントモジュールは、プロバイダーモジュールの[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)関数に対してそれ以上の呼び出しを行うことはできません。 クライアントモジュールの*ClientDetachProvider* callback 関数が呼び出されたときに、プロバイダーモジュールの NPI 関数のいずれかに対して実行中の呼び出しがない場合、 *ClientDetachProvider* callback 関数は状態を返す必要があり\_ブランド.

クライアントモジュールの[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数が呼び出されたときに、1つ以上のプロバイダーモジュールの NPI 関数への呼び出しが進行中の場合、 *ClientDetachProvider* callback 関数は状態を返す必要があり\_行わ. この場合、クライアントモジュールは、プロバイダーモジュールの NPI 関数の実行中のすべての呼び出しが完了した後に、 [**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)関数を呼び出す必要があります。 **NmrClientDetachProviderComplete**を呼び出すと、プロバイダーモジュールからのクライアントモジュールのデタッチが完了したことが NMR に通知されます。

プロバイダーモジュールの NPI 関数の実行中の呼び出しの数を追跡する方法の詳細については、「[プログラミングの考慮事項](programming-considerations.md)」を参照してください。

クライアントモジュールが[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn) callback 関数を実装している場合、NMR は、クライアントモジュールとプロバイダーモジュールの両方が完了した後に、クライアントモジュールの*ClientCleanupBindingContext*コールバック関数を呼び出します。相互にデタッチ。 クライアントモジュールの*ClientCleanupBindingContext* callback 関数は、クライアントモジュールのバインディングコンテキスト構造内に含まれるデータの必要なクリーンアップを実行する必要があります。 その後、クライアントモジュールが構造体のメモリを動的に割り当てた場合、バインドコンテキストの構造に対してメモリを解放する必要があります。

例:

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

 

 





