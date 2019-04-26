---
title: WSK クライアントの登録解除とアンロード
description: WSK クライアントの登録解除とアンロード
ms.assetid: dd9030b1-271f-46e4-9139-b49903ca8313
keywords:
- ネットワーク モジュール レジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0df3b4cbc19b082553bec52093ba7f201c77329
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340916"
---
# <a name="unregistering-and-unloading-the-wsk-client"></a>WSK クライアントの登録解除とアンロード


使用するアプリケーションは、Winsock カーネル (WSK)、[ネットワーク モジュール レジストラー (NMR)](network-module-registrar2.md) WSK へのアタッチのサブシステムはアンロードの前に解除 NMR にする必要があります。 ときに WSK アプリケーションの登録を解除、NMR で呼び出すことによって、 [ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)関数の場合、NMR を呼び出すアプリケーションの[ *ClientDetachProvider*](https://msdn.microsoft.com/library/windows/hardware/ff544908)コールバック関数、アプリケーションがそれ自体を WSK アプリケーションの登録解除プロセスの一環として、WSK サブシステムからデタッチされるようにします。

さらに、登録を解除すると、NMR WSK サブシステムの可能性は低いが、可能な場合は、NMR も呼び出して、WSK アプリケーションの*ClientDetachProvider*コールバック関数自体から、アプリケーションをデタッチするため、WSK サブシステムの登録解除プロセスの一環として WSK サブシステムです。

NMR 呼び出し WSK アプリケーションの*ClientDetachProvider*コールバック関数を 1 回だけです。 WSK アプリケーションと WSK サブシステムの両方が、NMR で登録解除、NMR 呼び出します WSK アプリケーションの*ClientDetachProvider*コールバック関数の最初の登録解除が開始された後のみです。

WSK WSK 関数のいずれかに進行中の呼び出しがない場合\_プロバイダー\_、NMR WSK アプリケーションの呼び出し時にディスパッチ*ClientDetachProvider*コールバック関数、WSK アプリケーション状態を返す必要があります\_成功からその*ClientDetachProvider*コールバック関数。 それ以外の場合、WSK アプリケーションは状態を返す必要があります\_PENDING からその*ClientDetachProvider*コールバック関数、およびそれを呼び出す必要があります、 [ **NmrClientDetachProviderComplete**](https://msdn.microsoft.com/library/windows/hardware/ff568772)関数結局、WSK を実行中の呼び出しの関数の WSK\_プロバイダー\_ディスパッチが返されます。 WSK アプリケーションが呼び出す、 **NmrClientDetachProviderComplete** WSK サブシステムから、アプリケーションがデタッチされている NMR に通知します。 ただし、WSK サブシステムでは、すべての開いているソケットが WSK アプリケーションによって閉じられるまで完全に完了するデタッチ プロシージャは許可されません。 詳細については、次を参照してください。[ソケットを閉じて](closing-a-socket.md)します。

WSK アプリケーションは、NMR を通知がデタッチが完了すると後の状態を返すことによって、\_から成功の*ClientDetachProvider*コールバック関数または呼び出すことによって、 **NmrClientDetachProviderComplete**関数、WSK で、アプリケーションは WSK 関数のいずれかにさらに任意呼び出しを行う必要がない\_プロバイダー\_ディスパッチします。

WSK アプリケーションを実装している場合、 [ *ClientCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff544904)コールバック関数、NMR を呼び出すアプリケーションの*ClientCleanupBindingContext*コールバックWSK アプリケーションおよび WSK サブシステムの両方がお互いからのデタッチを完了してからの関数。 WSK アプリケーションの*ClientCleanupBindingContext*コールバック関数は、アプリケーションのバインド コンテキストの構造体に含まれるデータのために必要なクリーンアップを実行する必要があります。 バインド コンテキストの構造体のメモリは、アプリケーションは、構造のメモリを動的に割り当てられる場合そのに解放する必要があります。

例:

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

WSK アプリケーションの[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数では、アプリケーションがから登録解除されますを確認する必要があります、 [NMR](network-module-registrar2.md)アプリケーションは、システム メモリからアンロードする前にします。 WSK アプリケーションから返す必要がありますいないその*アンロード*まで、NMR から完全に登録解除がされた後に機能します。 場合に呼び出し**NmrDeregisterClient**ステータスを返します\_保留中、WSK アプリケーションを呼び出す必要があります、 **NmrWaitForClientDeregisterComplete**関数を登録解除のために待機するには返す前に完了、*アンロード*関数。

例:

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

WSK アプリケーションを呼び出す必要はありません**NmrDeregisterClient**内からその*アンロード*関数。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントの場合は、WSK アプリケーションのサブコンポーネントが非アクティブ化が WSK アプリケーションの登録を解除することがあります。 ただし、このような状況では、ドライバーする必要がありますもことを確認、WSK アプリケーションが完全にから登録解除された、NMR から戻る前にその*アンロード*関数。

 

 





