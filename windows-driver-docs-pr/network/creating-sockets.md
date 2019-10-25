---
title: ソケットの作成
description: ソケットの作成
ms.assetid: 84cd0503-15bd-401f-836c-1fdc8425d073
keywords:
- Winsock カーネル WDK ネットワーク、ソケット作成
- WSK WDK ネットワーク、ソケットの作成
- リスニングソケット WDK Winsock カーネル
- WskSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 792259a655d0b9c8904244dc5634176891db0d83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835019"
---
# <a name="creating-sockets"></a>ソケットの作成


Winsock カーネル (WSK) アプリケーションが WSK サブシステムに正常にアタッチされた後、ネットワーク i/o 操作に使用できるソケットを作成できます。 WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数を呼び出すことによってソケットを作成します。 **Wsksocket**関数は、 [**WSK\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)の**wsksocket**メンバーによってポイントされます。これは、wsk サブシステムから返された、添付ファイルの\_ディスパッチ構造体です。

WSK アプリケーションでは、新しいソケットを作成するたびに作成される WSK ソケットのカテゴリを指定する必要があります。 WSK ソケットカテゴリの詳細については、「 [Winsock カーネルソケットカテゴリ](winsock-kernel-socket-categories.md)」を参照してください。

WSK アプリケーションでは、新しいソケットを作成するたびに、アドレスファミリ、ソケットの種類、およびプロトコルも指定する必要があります。 WSK でサポートされているアドレスファミリの詳細については、「 [Wsk アドレスファミリ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))」を参照してください。

新しいソケットを作成する場合、WSK アプリケーションでソケットのイベントコールバック関数を有効にする場合は、ソケットコンテキスト値とクライアントディスパッチテーブル構造へのポインターを指定する必要があります。 ソケットでイベントコールバック関数を有効にする方法の詳細については、「[イベントコールバック関数の有効化と無効化](enabling-and-disabling-event-callback-functions.md)」を参照してください。

ソケットが正常に作成された場合、IRP の**Iostatus. 情報**フィールドには、新しいソケットのソケットオブジェクト構造 ( [**wsk\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)) へのポインターが含まれます。 WSK 関数での Irp の使用の詳細については、「 [Winsock カーネル関数での irp の使用](using-irps-with-winsock-kernel-functions.md)」を参照してください。

次のコード例は、WSK アプリケーションでリッスンソケットを作成する方法を示しています。

```C++
// Context structure for each socket
typedef struct _WSK_APP_SOCKET_CONTEXT {
  PWSK_SOCKET Socket;
  .
  .  // Other application-specific members
  .
} WSK_APP_SOCKET_CONTEXT, *PWSK_APP_SOCKET_CONTEXT;

// Prototype for the socket creation IoCompletion routine
NTSTATUS
  CreateListeningSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to create a new listening socket
NTSTATUS
  CreateListeningSocket(
    PWSK_PROVIDER_NPI WskProviderNpi,
    PWSK_APP_SOCKET_CONTEXT SocketContext,
    PWSK_CLIENT_LISTEN_DISPATCH Dispatch,
    )
{
  PIRP Irp;
  NTSTATUS Status;

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
    CreateListeningSocketComplete,
    SocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the creation of the socket
  Status =
    WskProviderNpi->Dispatch->
        WskSocket(
          WskProviderNpi->Client,
          AF_INET,
          SOCK_STREAM,
          IPPROTO_TCP,
          WSK_FLAG_LISTEN_SOCKET,
          SocketContext,
          Dispatch,
          NULL,
          NULL,
          NULL,
          Irp
          );

  // Return the status of the call to WskSocket()
  return Status;
}

// Socket creation IoCompletion routine
NTSTATUS
  CreateListeningSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check the result of the socket creation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)Context;

    // Save the socket object for the new socket
    SocketContext->Socket =
      (PWSK_SOCKET)(Irp->IoStatus.Information);

    // Set any socket options for the new socket
    ...

    // Enable any event callback functions on the new socket
    ...

    // Perform any other initializations
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

接続指向のソケットの場合、WSK アプリケーションは[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して、1つの関数呼び出しでソケットを作成、バインド、および接続することができます。

 

 





