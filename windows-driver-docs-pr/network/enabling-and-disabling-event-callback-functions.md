---
title: イベント コールバック関数の有効化と無効化
description: イベント コールバック関数の有効化と無効化
ms.assetid: 52654788-31e2-47c1-8154-f40c42168708
keywords:
- ネットワーク、WSK WDK イベント
- WDK Winsock カーネル イベント
- WDK Winsock Kernel 関数
- WDK Winsock Kernel のイベントのコールバック関数
- SO_WSK_EVENT_CALLBACK
- WSK_SET_STATIC_EVENT_CALLBACKS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 093182ac87234a111f9268a78e33053c5e4beb14
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349619"
---
# <a name="enabling-and-disabling-event-callback-functions"></a>イベント コールバック関数の有効化と無効化


Winsock カーネル (WSK) アプリケーションは、WSK サブシステムを呼び出すときに特定のアプリケーションに通知を非同期的にイベントのコールバック関数を実装できます[イベント](winsock-kernel-events.md)ソケットで発生します。 WSK アプリケーションがクライアントに提供できます[ディスパッチ テーブル](winsock-kernel-dispatch-tables.md)WSK サブシステムにソケットを作成またはリッスン ソケットのソケットを受け入れるたびに構造体。 このディスパッチ テーブルには、新しいソケットの WSK アプリケーションのイベントのコールバック関数へのポインターが含まれています。 WSK アプリケーションが特定のソケットのイベントのコールバック関数を実装しないかどうかは、クライアントを提供する必要はありません、ソケットの WSK サブシステムにテーブル構造をディスパッチします。

すべての待機中のソケットを除く、ソケットのイベントのコールバック関数[ *WskInspectEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571137)と[ *WskAbortEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571108)イベントコールバック関数を有効になっているまたはを使用して無効になっていることができます、 [**ように\_WSK\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff570834)ソケット オプション。 WSK アプリケーションは、同時に、ソケットでの複数のイベントのコールバック関数を有効にできます。 ただし、WSK アプリケーションは各イベントのコールバック関数を個別に無効する必要があります。

次のコード例は、WSK アプリケーションが、これを使用する方法を示しています\_WSK\_イベント\_コールバックのソケット オプションを有効にする、 [ *WskDisconnectEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571130)と。[ *WskReceiveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571140)接続指向のソケットでのイベントのコールバック関数。

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

次のコード例は、WSK アプリケーションの使用方法を示しています、 [**ように\_WSK\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff570834)ソケットを無効にするオプション、 [ *WskReceiveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571140)接続指向のソケットでのイベントのコールバック関数。

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

リッスン ソケットの場合、 [ *WskInspectEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571137)と[ *WskAbortEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571108)場合にのみ、イベントのコールバック関数が有効になっている、WSK条件付きのアプリケーションによりは受け入れソケットのモードです。 WSK アプリケーションにより条件付きでは、リスナ ソケットでモードを受け入れるを設定して、 [**ように\_条件付き\_ACCEPT** ](https://msdn.microsoft.com/library/windows/hardware/ff570829)ソケットをバインドする前に、ソケット オプション、ローカル トランスポート アドレスするソケット。 ソケット オプションを設定する方法の詳細については、次を参照してください。[ソケットで管理操作を実行する](performing-control-operations-on-a-socket.md)します。

条件に同意をリッスンしているのモードが有効になって後ソケット、ソケットの*WskInspectEvent*と*WskAbortEvent*イベント コールバック関数を無効にすることはできません。 条件付きでリッスンしているソケットでの着信接続の受け入れの詳細については、次を参照してください。[リッスン中の接続と着信接続を受け入れる](listening-for-and-accepting-incoming-connections.md)します。

リッスン ソケットは接続指向のソケットでリッスン ソケットの受け入れられるでイベントのコールバック関数を自動的に有効に[ *WskAcceptEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571120)イベント コールバック関数。 WSK アプリケーションは、リッスン ソケットの接続指向のソケット イベント コールバック関数を有効にすると、これらのコールバック関数を自動的に有効です。 このプロセスの詳細については、次を参照してください。 [**ように\_WSK\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff570834)します。

アプリケーションを使用して、それらのイベントのコールバック関数を自動的に有効にする WSK サブシステムを構成できます WSK アプリケーションは常に、特定のイベント コールバック関数で作成されたすべてのソケットでは可能である場合、 [ **WSK\_設定\_静的\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff571181)クライアント管理の操作。 この方法で有効になっているイベントのコールバック関数は常に有効になっていると、無効になっているまたは WSK アプリケーションを後で再度有効にすることはできません。 WSK アプリケーションは常に、特定のイベント コールバック関数で作成されたすべてのソケットでは可能である場合でこのメソッドを使用してパフォーマンスをより向上が生成されますので、これらのイベントのコールバック関数を自動的に有効にする必要があります。

次のコード例は、WSK アプリケーションが、WSK を使用する方法を示しています\_設定\_静的\_イベント\_自動的に有効にするコールバック クライアント管理の操作、 [  *。WskReceiveFromEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571142)データグラム ソケットでのイベントのコールバック関数と[ *WskReceiveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571140)接続指向のイベントのコールバック関数ソケット。

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

WSK アプリケーション、WSK を使用している場合\_設定\_静的\_イベント\_特定イベントのコールバック関数を自動的に有効にするコールバック クライアント コントロールの操作、ソケットを作成する前にする必要があります。

 

 





