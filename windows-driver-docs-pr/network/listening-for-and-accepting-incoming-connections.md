---
title: 着信接続のリッスンと受け入れ
description: 着信接続のリッスンと受け入れ
ms.assetid: 3ec7d6d0-8b8c-4d98-9e2a-e42b52dcd544
keywords:
- Winsock カーネル WDK ネットワーク、着信接続
- WSK WDK ネットワーク、着信接続
- 着信接続 WDK Winsock カーネル
- リスニングソケット WDK Winsock カーネル
- 条件付き受け入れ WDK Winsock カーネル
- リッスン操作 WDK Winsock カーネル
- SO_CONDITIONAL_ACCEPT
- 接続の受け入れ WDK Winsock カーネル
- WskAccept
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd1b3d6d19f45459402e35b24cf507a6fc4d5665
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844145"
---
# <a name="listening-for-and-accepting-incoming-connections"></a>着信接続のリッスンと受け入れ


Winsock カーネル (WSK) アプリケーションがリッスンソケットをローカルトランスポートアドレスにバインドした後、ソケットはリモートトランスポートアドレスからの着信接続のリッスンを開始します。 WSK アプリケーションは、 [**Wskaccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)関数を呼び出すことによって、リスニングソケット上の着信接続を受け入れることができます。 アプリケーションが**Wskaccept**関数に渡す IRP は、受信接続が到着するまでキューに入れられます。

次のコード例は、WSK アプリケーションが**Wskaccept**関数を呼び出すことによって受信接続を受け入れる方法を示しています。

```C++
// Prototype for the accept IoCompletion routine
NTSTATUS
  AcceptComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to accept an incoming connection
NTSTATUS
  AcceptConnection(
    PWSK_SOCKET Socket,
    PVOID AcceptSocketContext,
    PWSK_CLIENT_CONNECTION_DISPATCH AcceptSocketDispatch
    )
{
  PWSK_PROVIDER_LISTEN_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_LISTEN_DISPATCH)(Socket->Dispatch);

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
    AcceptComplete,
    AcceptSocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the accept operation on the socket
  Status =
    Dispatch->WskAccept(
      Socket,
      0,  // No flags
      AcceptSocketContext,
      AcceptSocketDispatch,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskAccept()
  return Status;
}

// The accept IoCompletion routine
NTSTATUS
  AcceptComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;
  PVOID AcceptSocketContext;

  // Check the result of the accept operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the accepted socket object from the IRP
    Socket = (PWSK_SOCKET)(Irp->IoStatus.Information);

    // Get the accepted socket's context
    AcceptSocketContext = Context;

    // Perform the next operation on the accepted socket
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

リッスンソケットでの受信接続を受け入れるために[**Wskaccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)関数を呼び出す代わりに、wsk アプリケーションでは、そのソケットで[*wskacceptevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)イベントコールバック関数を有効にすることができます。 WSK アプリケーションで、リッスンしているソケットで*Wskacceptevent*のイベントコールバック関数が有効になっている場合、wsk サブシステムは、新しい着信接続がソケットで受け入れられるたびに、*そのイベントコール*バック関数を呼び出します。 リスニングソケットの*Wskacceptevent*イベントコールバック関数を有効にする方法の詳細については、「[イベントコールバック関数の有効化と無効化](enabling-and-disabling-event-callback-functions.md)」を参照してください。

次のコード例では、WSK アプリケーションがリッスンソケットの*Wskacceptevent*イベントコールバック関数を呼び出す wsk サブシステムによる受信接続を受け入れる方法を示します。

```cpp
// Dispatch table of event callback functions for accepted sockets
const WSK_CLIENT_CONNECTION_DISPATCH ConnectionDispatch =
{
  .
  . // Function pointers for the event callback functions
  .
};

// Pool tag used for allocating the socket context
#define SOCKET_CONTEXT_POOL_TAG 'tpcs'

// A listening socket's WskAcceptEvent event callback function
NTSTATUS WSKAPI
  WskAcceptEvent(
    PVOID SocketContext,
    ULONG Flags,
    PSOCKADDR LocalAddress,
    PSOCKADDR RemoteAddress,
    PWSK_SOCKET AcceptSocket,
    PVOID *AcceptSocketContext,
    CONST WSK_CLIENT_CONNECTION_DISPATCH **AcceptSocketDispatch
    )
{
  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check for a valid new socket
  if (AcceptSocket != NULL)
  {
    // Allocate the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)
        ExAllocatePoolWithTag(
          NonPagedPool,
          sizeof(WSK_APP_SOCKET_CONTEXT),
          SOCKET_CONTEXT_POOL_TAG
          );

    // Check result of allocation
    if (SocketContext == NULL)
    {
      // Reject the socket
      return STATUS_REQUEST_NOT_ACCEPTED;
    }

    // Initialize the socket context
    SocketContext->Socket = AcceptSocket;
    ...

    // Set the accepted socket's client context
    *AcceptSocketContext = SocketContext;

    // Set the accepted socket's dispatch table of callback functions
    *AcceptSocketDispatch = ConnectionDispatch;

    // Perform additional operations on the accepted socket
    ...

    // Return status indicating that the socket was accepted
    return STATUS_SUCCESS:
  }

  // Error with listening socket
  else
  {
    // Handle error
    ...

    // Return status indicating that no socket was accepted
    return STATUS_REQUEST_NOT_ACCEPTED;
  }
}
```

WSK アプリケーションでは、ソケットで受信した着信接続を条件付きで受け入れられるようにリッスンソケットを構成できます。 WSK アプリケーションでは、ソケットをローカルトランスポートアドレスにバインドする前に、ソケットの[ **\_条件付き\_accept**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept)ソケットオプションを設定することにより、リッスンソケットで条件付き受け入れモードを有効にします。 ソケットオプションの設定方法の詳細については、「[ソケットでの制御操作の実行](performing-control-operations-on-a-socket.md)」を参照してください。

待機中のソケットで条件付き受け入れモードが有効になっている場合、WSK サブシステムは、新しい受信接続要求がソケットで受信されるたびに、最初にソケットの[*WskInspectEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)イベントコールバック関数を呼び出します。 ソケットの*WskInspectEvent*イベントコールバック関数は、受信接続要求を検査して、要求を受け入れるか拒否するかを決定できます。 要求を受け入れるために、ソケットの*WskInspectEvent*イベントコールバック関数は**InspectAccept**を返します。 要求を拒否するために、ソケットの*WskInspectEvent*イベントコールバック関数は**InspectReject**を返します。 ソケットの*WskInspectEvent*イベントコールバック関数が要求を受け入れるか拒否するかをすぐに判断できない場合は、 **InspectPend**を返します。 このような状況では、WSK アプリケーションは、受信接続要求の検査プロセスの完了後に[**WskInspectComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_complete)関数を呼び出す必要があります。 ソケット接続が完全に確立される前に受信接続要求が削除された場合、WSK サブシステムは WSK アプリケーションの[*Wskabortevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)イベントコールバック関数を呼び出します。

次のコード例は、WSK アプリケーションがリッスンソケットの*WskInspectEvent*イベントコールバック関数を呼び出して wsk サブシステムによって受信接続要求を検査する方法を示しています。

```C++
// Inspect ID for a pending inspection
WSK_INSPECT_ID PendingInspectID

// A listening socket's WskInspectEvent event callback function
WSK_INSPECT_ACTION WSKAPI
  WskInspectEvent(
    PVOID SocketContext,
    PSOCKADDR LocalAddress,
    PSOCKADDR RemoteAddress,
    PWSK_INSPECT_ID InspectID
    )
{
  // Check for a valid inspect ID
  if (InspectID != NULL)
  {
    // Inspect local and/or remote address of the incoming
    // connection request to determine if the connection should
    // be accepted or rejected.
    ...

    // If the incoming connection should be accepted
    if (...)
    {
      // Return status indicating that the incoming
      // connection request was accepted
      return InspectAccept;
    }

    // If the incoming connection should be rejected
    else if (...)
    {
      // Return status indicating that the incoming
      // connection request was rejected
      return InspectReject;
    }

    // Cannot determine immediately
    else
    {
      // Save the inspect ID while the inspection is pending.
      // This will be passed to WskInspectComplete when the
      // inspection process is completed.
      PendingInspectID = *InspectID;

      // Return status indicating that the result of the
      // inspection process for the incoming connection
      // request is pending
      return InspectPend;
    }
  }

  // Error with listening socket
  else
  {
    // Handle error
    ...

    // Return status indicating that a socket was not accepted
    return InspectReject;
  }
}

// A listening socket's WskAbortEvent event callback function
NTSTATUS WSKAPI
  WskAbortEvent(
    PVOID SocketContext,
    PWSK_INSPECT_ID InspectID
    )
{
  // Terminate the inspection for the incoming connection
  // request with a matching inspect ID. To test for a matching
  // inspect ID, the contents of the WSK_INSPECT_ID structures
  // must be compared, not the pointers to the structures.
  ...
}
```

WSK アプリケーションが、条件付き受け入れモードが有効になっているリスニングソケットで受信接続要求を受け入れることを判断した場合、受信接続が確立されます。これは、アプリケーションが前に説明したように、 [**Wskaccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)関数またはソケットの[*wskacceptevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)イベントコールバック関数を呼び出す wsk サブシステム。

 

 





