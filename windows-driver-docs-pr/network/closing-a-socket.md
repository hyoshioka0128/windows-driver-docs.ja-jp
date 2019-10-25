---
title: ソケットを閉じる
description: ソケットを閉じる
ms.assetid: 3fa2d5c3-7b52-4bbe-b99d-ef3be19c7c7e
keywords:
- Winsock カーネル WDK ネットワーク、ソケットの終了
- WSK WDK ネットワーク、ソケットの終了
- ソケットを閉じる
- WskCloseSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f76372dbd8e8dc160ea8988d25f23b1671f21e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835161"
---
# <a name="closing-a-socket"></a>ソケットを閉じる


Winsock カーネル (WSK) アプリケーションでソケットの使用が完了したら、ソケットを閉じ、関連付けられているすべてのリソースを解放する必要があります。 WSK アプリケーションは、WSK サブシステムからアプリケーションをデタッチする前に、開いているすべてのソケットを閉じる必要があります。 Wsk アプリケーションを WSK サブシステムからデタッチする方法の詳細については、「 [Winsock カーネルアプリケーションの登録解除](unregistering-a-winsock-kernel-application.md)」を参照してください。

WSK アプリケーションは、 [**Wskclosesocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)関数を呼び出すことによってソケットを閉じます。 WSK アプリケーションは、 **Wskclosesocket**関数を呼び出す前に、任意のアプリケーションの他のスレッドの拡張関数を含め、どのソケットの関数にも他の関数呼び出しが実行されていないことを確認する必要があります。 ただし、まだ完了していないソケットの関数を以前に呼び出した場合、WSK アプリケーションは**Wskclosesocket**を呼び出すことができます。

WSK アプリケーションが、 **Wskclosesocket**関数を呼び出す前に、ソケットの関数のいずれかに対して実行中の他の関数呼び出しがないことを確認するために使用するメソッドは、アプリケーションの設計に依存します。 たとえば、WSK アプリケーションで1つのスレッドでソケットを閉じる必要がある場合に、そのソケットの他のスレッドの他の関数に対して呼び出しが進行中である可能性があります。その場合、アプリケーションは通常、参照カウンターを使用して関数の数を追跡します。ソケットで現在実行中の呼び出し。 このような状況では、WSK アプリケーションは、ソケットの関数の1つを呼び出す前に、ソケットの参照カウンターをアトミックにテストしてインクリメントし、関数から制御が戻ったときに、ソケットの参照カウンターをアトミックにデクリメントします。 参照カウンターがゼロの場合、WSK アプリケーションは**Wskclosesocket**関数を安全に呼び出し、ソケットを閉じることができます。

一方、WSK アプリケーションの設計によって、他のスレッドの特定のソケットの関数の呼び出しが行われないことが、アプリケーションから**Wskclosesocket**関数が呼び出されてソケットが閉じられる場合は、wsk が使用されます。アプリケーションでは、参照カウンターを使用して、ソケットで現在実行中の関数呼び出しの数を追跡する必要はありません。 たとえば、WSK アプリケーションが1つのスレッドから特定のソケットに対してすべてのソケット操作を実行する場合、アプリケーションは参照カウンターを必要とせずに、そのスレッド内から**Wskclosesocket**関数を安全に呼び出すことができます。

**Wskclosesocket**関数を呼び出すと、wsk サブシステムは、ソケットの関数に対する以前の呼び出しから、すべての保留中の irp を取り消して完了します。 WSK サブシステムでは、close 操作が完了する前に、進行中のイベントコールバック関数が WSK サブシステムに制御を戻したことも保証されます。

次のコード例は、WSK アプリケーションでソケットを閉じる方法を示しています。

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

WSK アプリケーションが[**Wskclosesocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)を呼び出した後は、ソケットの関数をそれ以上呼び出すことはできません。

WSK アプリケーションが、以前に両方の方向に切断されていない接続指向のソケットを閉じると、WSK サブシステムはソケットを閉じる前に、ソケットの切断を自動的に実行します。 ソケットの切断の詳細については、「[宛先からのソケットの切断](disconnecting-a-socket-from-a-destination.md)」を参照してください。

 

 





