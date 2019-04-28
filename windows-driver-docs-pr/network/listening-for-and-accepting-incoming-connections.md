---
title: 着信接続のリッスンと受け入れ
description: 着信接続のリッスンと受け入れ
ms.assetid: 3ec7d6d0-8b8c-4d98-9e2a-e42b52dcd544
keywords:
- Winsock カーネル WDK、着信ネットワーク接続
- WSK WDK、着信ネットワーク接続
- WDK Winsock Kernel の着信接続
- リッスンしているソケット WDK Winsock カーネル
- 条件付き受け入れ WDK Winsock カーネル
- リッスン操作 WDK Winsock カーネル
- SO_CONDITIONAL_ACCEPT
- WDK Winsock Kernel の接続の受け入れ
- WskAccept
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52b327b972090ef5be6981e79bcf1b9bd290584
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362326"
---
# <a name="listening-for-and-accepting-incoming-connections"></a>着信接続のリッスンと受け入れ


Winsock カーネル (WSK) アプリケーションでは、ローカル トランスポート アドレスをリッスン ソケットがバインド、ソケットがリモートのトランスポート アドレスからの着信接続のリッスン開始されます。 呼び出して WSK アプリケーションがリッスン ソケットの受信接続を受け入れることができます、 [ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)関数。 アプリケーションに渡す IRP、 **WskAccept**関数には、着信接続が到着するまではキューに配置します。

次のコード例は呼び出すことによって、WSK アプリケーションが着信接続を受け付ける方法を示しています、 **WskAccept**関数。

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

呼び出す代わりとして、 [ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)リスナ ソケットでの着信接続を受け入れる関数、WSK アプリケーションを有効にすることができます、 [ *WskAcceptEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571120)ソケットでのイベントのコールバック関数。 WSK アプリケーションを使用する場合、 *WskAcceptEvent*リスナ ソケットでのイベントのコールバック関数、WSK サブシステムを呼び出す、ソケットの*WskAcceptEvent*たびに新しい受信のイベントのコールバック関数接続は、ソケットで許可されます。 リッスン ソケットの有効化の詳細については*WskAcceptEvent*イベントのコールバック関数を参照してください[の有効化と無効にするとイベントのコールバック関数](enabling-and-disabling-event-callback-functions.md)します。

次のコード例は、WSK サブシステムを待機中のソケットを呼び出すことによって、WSK アプリケーションが着信接続を承諾する方法を示しています。 *WskAcceptEvent*イベント コールバック関数。

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

WSK アプリケーションでは、条件付きでソケットに受信した着信接続を受け入れるように待機中のソケットを構成できます。 WSK アプリケーションにより条件付きでは、リスナ ソケットでモードを受け入れるを設定して、 [**ように\_条件付き\_ACCEPT** ](https://msdn.microsoft.com/library/windows/hardware/ff570829)ソケットをバインドする前に、ソケット オプション、ローカル トランスポート アドレスするソケット。 ソケット オプションを設定する方法の詳細については、次を参照してください。[ソケットで管理操作を実行する](performing-control-operations-on-a-socket.md)します。

WSK サブシステムが、ソケットの最初を呼び出す条件に同意リッスン ソケットのモードが有効になっている場合、 [ *WskInspectEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571137)新しい着信接続要求されるたびに、イベント コールバック関数ソケットの受信します。 ソケットの*WskInspectEvent*イベント コールバック関数は、要求を受け入れるか拒否されたかどうかを決定する受信接続要求を検査できます。 要求を受け入れる、ソケットの*WskInspectEvent*イベント コールバック関数が返す**InspectAccept**します。 要求を拒否する、ソケットの*WskInspectEvent*イベント コールバック関数が返す**InspectReject**します。 ソケットの場合、 *WskInspectEvent*返しますイベント コールバック関数は、要求を受け入れるか拒否された場合にすぐに判定することはできません、 **InspectPend**します。 このような状況で WSK アプリケーションを呼び出す必要があります、 [ **WskInspectComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff571136)関数の着信接続要求の検査プロセスの完了後します。 WSK サブシステムが WSK アプリケーションを呼び出す場合は、受信接続要求が削除されるは、ソケット接続が完全に確立される前に、 [ *WskAbortEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571108)イベント コールバック関数。

次のコード例は、呼び出しのリッスン ソケットの WSK サブシステムによって、WSK アプリケーションが、受信接続要求を検査する方法を示しています。 *WskInspectEvent*イベント コールバック関数。

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

着信接続が確立され、アプリケーションを呼び出すことによって通常受け入れられることができます WSK アプリケーションを有効になっているモードをそのまま使用条件を持つリッスン ソケットの受信接続要求を受け付けることを判断した場合、[ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)関数または呼び出しのソケットの WSK サブシステム[ *WskAcceptEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571120)イベント コールバック関数の説明に従って先に。

 

 





