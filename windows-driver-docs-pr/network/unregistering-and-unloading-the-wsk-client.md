---
title: WSK クライアントの登録解除とアンロード
description: WSK クライアントの登録解除とアンロード
ms.assetid: dd9030b1-271f-46e4-9139-b49903ca8313
keywords:
- ネットワークモジュールレジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5723f955787a0e2e73ddb701ee0c3a559aad12e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843001"
---
# <a name="unregistering-and-unloading-the-wsk-client"></a>WSK クライアントの登録解除とアンロード


WSK サブシステムへのアタッチに[ネットワークモジュールレジストラー (NMR)](network-module-registrar2.md)を使用するすべての Winsock カーネル (wsk) アプリケーションは、アンロードの前に NMR で登録を解除する必要があります。 WSK アプリケーションが[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)関数を呼び出すことによって NMR で登録を解除すると、NMR はアプリケーションの[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数を呼び出します。これにより、アプリケーションは、アプリケーションが wsk サブシステムから、WSK アプリケーションの登録解除プロセス。

さらに、可能性はほとんどありませんが、WSK サブシステムが NMR に登録を解除した場合、NMR は WSK アプリケーションの*ClientDetachProvider*コールバック関数も呼び出します。これにより、アプリケーションは wsk サブシステムからアプリケーションをデタッチできます。WSK サブシステムの登録解除プロセス。

NMR は WSK アプリケーションの*ClientDetachProvider* callback 関数を1回だけ呼び出します。 WSK アプリケーションと WSK サブシステムの両方が NMR の登録を解除した場合、NMR は最初の登録解除が開始された後に WSK アプリケーションの*ClientDetachProvider* callback 関数を呼び出します。

Wsk\_\_PROVIDER の WSK 関数のいずれかに対して実行中の呼び出しがない場合は、NMR が WSK アプリケーションの*ClientDetachProvider*コールバック関数を呼び出したときに、wsk アプリケーションがステータスを返す必要があり\_*ClientDetachProvider* callback 関数による成功。 それ以外の場合、WSK アプリケーションは*ClientDetachProvider* callback 関数から STATUS\_PENDING を返す必要があります。また、 [**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)関数は、実行中のすべての呼び出しをの wsk 関数に呼び出した後に呼び出す必要があります。WSK\_プロバイダー\_ディスパッチが返されました。 WSK アプリケーションは、 **NmrClientDetachProviderComplete**関数を呼び出して、アプリケーションが wsk サブシステムからデタッチされたことを NMR に通知します。 ただし、WSK サブシステムでは、すべての開いているソケットが WSK アプリケーションによって閉じられるまで、デタッチプロシージャを完全に完了することはできません。 詳細については、「[ソケットを閉じる](closing-a-socket.md)」を参照してください。

WSK アプリケーションがデタッチが完了したことを NMR に通知した後、 *ClientDetachProvider*コールバック関数から STATUS\_SUCCESS を返すか、 **NmrClientDetachProviderComplete**関数を呼び出します。アプリケーションでは、WSK\_プロバイダー\_ディスパッチの WSK 関数のいずれかに対してそれ以上の呼び出しを行うことはできません。

WSK アプリケーションで[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn) callback 関数が実装されている場合、wsk アプリケーションと wsk サブシステムの両方が完了した後、NMR はアプリケーションの*ClientCleanupBindingContext*コールバック関数を呼び出します。相互にデタッチ。 WSK アプリケーションの*ClientCleanupBindingContext*コールバック関数は、アプリケーションのバインディングコンテキスト構造内に含まれるデータの必要なクリーンアップを実行する必要があります。 その後、アプリケーションが構造体に対して動的に割り当てられたメモリを使用している場合は、バインディングコンテキストの構造に対してメモリを解放する必要があります。

次に、例を示します。

```C++
// ClientDetachProvider callback function
NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    )
{
  PWSK_APP_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)ClientBindingContext;

  // Check if there are no calls in progress to any WSK functions
  // in WSK_PROVIDER_DISPATCH and that there are no open sockets
  if (...)
  {
    // Return success status indicating that detachment is complete
    return STATUS_SUCCESS;
  }

  // There are calls in progress to one or more of the WSK functions
  // in WSK_PROVIDER_DISPATCH and/or one or more open sockets
  else
  {
    // Return pending status, indicating that detachment is pending
    // completion of the calls in progress to the WSK functions in
    // WSK_PROVIDER_DISPATCH and/or closing of the open sockets
    return STATUS_PENDING;

    // When all of the calls in progress to the WSK functions
    // in WSK_PROVIDER_DISPATCH are completed, the WSK application
    // must close all open sockets.
    //
    // After all sockets have been closed, the WSK application must
    // call the NmrClientDetachProviderComplete function with the
    // binding handle for the attachment to the WSK subsystem.
  }
}

// ClientCleanupBindingContext callback function
VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    )
{
  PWSK_APP_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)ClientBindingContext;

  // Clean up the binding context structure
  ...

  // Free the memory for client's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

WSK アプリケーションの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数は、アプリケーションがシステムメモリからアンロードされる前に、アプリケーションが[NMR](network-module-registrar2.md)から登録解除されていることを確認する必要があります。 WSK アプリケーションは、NMR から完全に登録解除されるまで、 *Unload*関数から戻ることはできません。 **NmrDeregisterClient**の呼び出しで STATUS\_PENDING が返された場合、wsk アプリケーションは、*アンロード*から戻る前に登録解除が完了するまで待機するために、 **NmrWaitForClientDeregisterComplete**関数を呼び出す必要があります。プロシージャ.

次に、例を示します。

```C++
// Variable containing the handle for registration with the NMR
HANDLE RegistrationHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Unregister the WSK application from the NMR
  Status =
    NmrDeregisterClient(
      RegistrationHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the unregistration to be completed
    NmrWaitForClientDeregisterComplete(
      RegistrationHandle
      );
  }
}
```

WSK アプリケーションは、 *Unload*関数内から**NmrDeregisterClient**を呼び出す必要はありません。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントである場合、wsk アプリケーションのサブコンポーネントが非アクティブになると WSK アプリケーションの登録が解除されることがあります。 ただし、このような状況でも、ドライバーは、*アンロード*関数から戻る前に、wsk アプリケーションが NMR から完全に登録解除されていることを確認する必要があります。

 

 





