---
title: ソケットを閉じる
description: ソケットを閉じる
ms.assetid: 3fa2d5c3-7b52-4bbe-b99d-ef3be19c7c7e
keywords:
- Winsock カーネル WDK のネットワーク、ソケットを閉じる
- WSK WDK ネットワーク、ソケットを閉じる
- ソケットを閉じる
- WskCloseSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe8478b6c685c125bab4f7b11e67906cb268c42
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350015"
---
# <a name="closing-a-socket"></a>ソケットを閉じる


Winsock カーネル (WSK) アプリケーションは、ソケットの使用が完了したらは、ソケットを閉じる必要があり、関連付けられたリソースを解放します。 WSK アプリケーションは、アプリケーションがそれ自体を WSK サブシステムからデタッチする前に、すべての開いているソケットを閉じる必要があります。 WSK サブシステムから WSK アプリケーションのデタッチに関する詳細については、次を参照してください。 [Winsock カーネル アプリケーションの登録を解除](unregistering-a-winsock-kernel-application.md)します。

WSK アプリケーションが呼び出すことによって、ソケットを閉じます、 [ **WskCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571124)関数。 呼び出しの前に、 **WskCloseSocket**関数、WSK アプリケーションの必要がありますようにに他の関数呼び出しなしに、アプリケーションのいずれかで、拡張関数を含む、ソケットの関数のいずれかに進行状況ほかはスレッド。 ただし、WSK アプリケーションを呼び出すことができます**WskCloseSocket**かどうかがある保留中の Irp をまだ完了していないソケットの関数の前の呼び出しから。

呼び出す前に、ソケットの関数のいずれかに進行中の WSK アプリケーションが他の関数がないことを確認に使用するメソッドを呼び出して、 **WskCloseSocket**関数は、アプリケーションの設計に依存します。 たとえば場合 WSK アプリケーションは、ソケットの進行中の呼び出しがある可能性がありますが、1 つのスレッドでソケットを閉じる必要があります 1 つまたは複数の他のスレッドでは、そのアプリケーションで他の関数は通常使用参照カウンター関数の数を追跡するには現在、ソケットで進行中の呼び出し。 このような状況で WSK アプリケーション アトミックに調べ、ソケットの関数の 1 つを呼び出すことと、アトミックにデクリメント ソケットの参照カウンターの場合に前に、ソケットの参照カウンターをインクリメントを返します。 参照カウンターが 0 の場合、WSK アプリケーションを安全に呼び出す、 **WskCloseSocket**ソケットを閉じます。

その一方、WSK アプリケーションの設計を保証がありますいない呼び出しを他のスレッド内の特定のソケットの関数の進行中のアプリケーションを呼び出すときの場合、 **WskCloseSocket**関数を閉じる、ソケット、WSK アプリケーションは、参照カウンターを使用して、現在、ソケットで進行中の関数呼び出しの数を追跡する必要はありません。 たとえば、WSK アプリケーションでは、1 つのスレッドからすべての特定のソケットに対してソケット操作を実行する場合、アプリケーションを安全に呼び出す、 **WskCloseSocket**を必要としないスレッド内で関数を参照カウンター。

呼び出す、 **WskCloseSocket**関数は、前のソケットの関数呼び出しからのすべての保留中の Irp の完了をキャンセルして WSK サブシステム。 WSK サブシステムは、閉じる操作が完了する前に、進行中のイベントのコールバック関数が WSK サブシステムにコントロールを返さことも確認します。

次のコード例では、WSK アプリケーションが、ソケットを閉じる方法を示します。

```C++
// Prototype for the socket close IoCompletion routine
NTSTATUS
  CloseSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to close a socket
NTSTATUS
  CloseSocket(
    PWSK_SOCKET Socket,
    PWSK_APP_SOCKET_CONTEXT SocketContext
    )
{
  PWSK_PROVIDER_BASIC_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_BASIC_DISPATCH)(Socket->Dispatch);

  // Allocate an IRP
  Irp =
    IoAllocateIrp(
      1,
      FALSE
      );

  // Check result
  if (!Irp)
  {
    // Return error
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Set the completion routine for the IRP
  IoSetCompletionRoutine(
    Irp,
    CloseSocketComplete,
    SocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the close operation on the socket
  Status =
    Dispatch->WskCloseSocket(
      Socket,
      Irp
      );

  // Return the status of the call to WskCloseSocket()
  return Status;
}

// Socket close IoCompletion routine
NTSTATUS
  CloseSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check the result of the socket close operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)Context;

    // Perform any cleanup and/or deallocation of the socket context
    ...
  }

  // Error status
  else
  {
    // Handle error
    ...
  }

  // Free the IRP
  IoFreeIrp(Irp);

  // Always return STATUS_MORE_PROCESSING_REQUIRED to
  // terminate the completion processing of the IRP.
  return STATUS_MORE_PROCESSING_REQUIRED;
}
```

アプリケーションが呼び出されて、WSK 後[ **WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)、さらに呼び出し、ソケットの関数のいずれかにしないようにします。

WSK アプリケーションでは、双方向で以前に切断されましたいない接続指向のソケットが閉じ、ソケットを閉じる前に、ソケットの中止になる切断は、WSK サブシステムによって自動的に実行します。 ソケットを切断しています。 詳細については、次を参照してください。[宛先からソケットを切断する](disconnecting-a-socket-from-a-destination.md)します。

 

 





