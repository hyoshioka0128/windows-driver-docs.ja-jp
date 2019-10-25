---
title: イベント コールバック関数の有効化と無効化
description: イベント コールバック関数の有効化と無効化
ms.assetid: 52654788-31e2-47c1-8154-f40c42168708
keywords:
- WSK WDK ネットワーク、イベント
- イベント WDK Winsock カーネル
- functions WDK Winsock カーネル
- イベントコールバック関数 WDK Winsock カーネル
- SO_WSK_EVENT_CALLBACK
- WSK_SET_STATIC_EVENT_CALLBACKS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 945b1986cf286943d01749501e5f90d3a381c637
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834788"
---
# <a name="enabling-and-disabling-event-callback-functions"></a>イベント コールバック関数の有効化と無効化


Winsock カーネル (WSK) アプリケーションでは、WSK サブシステムが非同期に呼び出して、特定の[イベント](winsock-kernel-events.md)がソケットで発生したときにアプリケーションに通知するイベントコールバック関数を実装できます。 WSK アプリケーションは、ソケットを作成するとき、またはリスニングソケット上のソケットを受け入れるたびに、クライアント[ディスパッチテーブル](winsock-kernel-dispatch-tables.md)構造を wsk サブシステムに提供できます。 このディスパッチテーブルには、新しいソケットの WSK アプリケーションのイベントコールバック関数へのポインターが含まれています。 WSK アプリケーションが特定のソケットに対してイベントコールバック関数を実装していない場合、そのソケットの WSK サブシステムにクライアントディスパッチテーブル構造を提供する必要はありません。

ソケットの[*WskInspectEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)および[*Wskabortevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)イベントコールバック関数を除き、ソケットのすべてのイベントコールバック関数を有効または無効にするには、 [ **\_WSK\_イベント\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)を使用します。socket オプション。 WSK アプリケーションでは、複数のイベントコールバック関数を1つのソケットで同時に有効にすることができます。 ただし、WSK アプリケーションでは、各イベントコールバック関数を個別に無効にする必要があります。

次のコード例は、WSK アプリケーションで\_WSK\_イベント\_コールバックソケットオプションを使用して、接続指向で[*Wskdisconnectevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event)イベントコールバック関数と[*wskdisconnectevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)イベントコールバック関数を有効にする方法を示しています。socket.

```C++
// Function to enable the WskDisconnectEvent and WskReceiveEvent
// event callback functions on a connection-oriented socket
NTSTATUS
  EnableDisconnectAndRecieveCallbacks(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flags for the event callback functions that
  // are to be enabled on the socket
  EventCallbackControl.EventMask =
    WSK_EVENT_DISCONNECT | WSK_EVENT_RECEIVE;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_WSK_EVENT_CALLBACK,
      SOL_SOCKET,
      sizeof(WSK_EVENT_CALLBACK_CONTROL),
      &EventCallbackControl,
      0,
      NULL,
      NULL,
      NULL  // No IRP for this control operation
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}
```

次のコード例は、WSK アプリケーションで[ **\_wsk\_イベント\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)ソケットオプションを使用して、接続指向のソケットで[*wskreceiveevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)イベントコールバック関数を無効にする方法を示しています。

```C++
// Prototype for the disable disconnect IoCompletion routine
NTSTATUS
  DisableDisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to disable the WskDisconnectEvent event
// callback functions on a connection-oriented socket
NTSTATUS
  DisableDisconnectCallback(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

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
 DisableDisconnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flag for the event callback function that
  // is to be disabled on the socket along with the disable flag
  EventCallbackControl.EventMask =
    WSK_EVENT_DISCONNECT | WSK_EVENT_DISABLE;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_WSK_EVENT_CALLBACK,
      SOL_SOCKET,
      sizeof(WSK_EVENT_CALLBACK_CONTROL),
      &EventCallbackControl,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Disable disconnect IoCompletion routine
NTSTATUS
  DisableDisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the control operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // The WskDisconnectEvent event callback
    // function is now disabled

    // Get the socket object from the context
    Socket = (PWSK_SOCKET)Context;

    // Perform the next operation on the socket
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

リッスンソケットの場合、 [*WskInspectEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)および[*wskabortevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)イベントコールバック関数は、wsk アプリケーションでソケットで条件付き受け入れモードが有効になっている場合にのみ有効になります。 WSK アプリケーションでは、ソケットをローカルトランスポートアドレスにバインドする前に、ソケットの[ **\_条件付き\_accept**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept)ソケットオプションを設定することにより、リッスンソケットで条件付き受け入れモードを有効にします。 ソケットオプションの設定方法の詳細については、「[ソケットでの制御操作の実行](performing-control-operations-on-a-socket.md)」を参照してください。

リスニングソケットで条件付き受け入れモードが有効になった後、ソケットの*WskInspectEvent*および*wskabortevent*イベントコールバック関数を無効にすることはできません。 リッスンソケットで着信接続を条件付きで受け入れる方法の詳細については、「[受信接続のリッスンと受け入れ](listening-for-and-accepting-incoming-connections.md)」を参照してください。

リッスンソケットは、リッスンしているソケットの[*Wskacceptevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)イベントコールバック関数によって受け入れられる接続指向のソケットに対して、イベントコールバック関数を自動的に有効にすることができます。 WSK アプリケーションは、リッスンしているソケットで接続指向のソケットイベントコールバック関数を有効にすることで、これらのコールバック関数を自動的に有効にします。 このプロセスの詳細については、「 [ **\_WSK\_イベント\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)」を参照してください。

WSK アプリケーションで、作成するすべてのソケットで特定のイベントコールバック関数が常に有効になっている場合、アプリケーションで wsk サブシステムを構成し、 [**wsk\_SET\_STATIC を使用してイベントコールバック関数を自動的に有効にすることができ @no__tイベント\_コールバッククライアントコントロール操作 (_s)** ](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-set-static-event-callbacks) 。 この方法で有効になっているイベントコールバック関数は常に有効になり、後で WSK アプリケーションで無効にしたり再度有効にしたりすることはできません。 WSK アプリケーションで、作成するすべてのソケットで特定のイベントコールバック関数が常に有効になっている場合、アプリケーションはこのメソッドを使用して、これらのイベントコールバック関数を自動的に有効にする必要があります。これにより、パフォーマンスが大幅に向上します。

次のコード例では、WSK アプリケーションが WSK\_設定\_静的\_イベント\_コールバッククライアントコントロール操作を使用して、データグラムで[*WskReceiveFromEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)イベントコールバック関数を自動的に有効にする方法を示します。接続指向のソケットでのソケットおよび[*Wskreceiveevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)イベントコールバック関数。

```C++
// Function to set static event callbacks
NTSTATUS
  SetStaticEventCallbacks(
    PWSK_APP_BINDING_CONTEXT BindingContext,
    )
{
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
  NTSTATUS Status;

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flags for the event callback functions that
  // are to be automatically enabled on every new socket
  EventCallbackControl.EventMask =
    WSK_EVENT_RECEIVE_FROM | WSK_EVENT_RECEIVE;

  // Perform client control operation
  Status =
    BindingContext->
      WskProviderDispatch->
        WskControlClient(
          BindingContext->WskClient,
          WSK_SET_STATIC_EVENT_CALLBACKS,
          sizeof(WSK_EVENT_CALLBACK_CONTROL),
          &EventCallbackControl,
          0,
          NULL,
          NULL,
          NULL  // No IRP for this control operation
          );

  // Return status of client control operation
  return Status;
}
```

WSK アプリケーションが WSK\_使用して\_静的\_イベント\_コールバッククライアントコントロール操作で特定のイベントコールバック関数を自動的に有効にする場合は、ソケットを作成する前に、それを実行する必要があります。

 

 





