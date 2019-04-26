---
title: ソケットの作成
description: ソケットの作成
ms.assetid: 84cd0503-15bd-401f-836c-1fdc8425d073
keywords:
- Winsock カーネル WDK がネットワーク、ソケットの作成
- WSK WDK ネットワーク、ソケットの作成
- リッスンしているソケット WDK Winsock カーネル
- WskSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52f3b71aaf46ad77ee7b9db0880a7ba0c970e894
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357238"
---
# <a name="creating-sockets"></a>ソケットの作成


後は、Winsock カーネル (WSK) アプリケーションが正常に WSK サブシステムにアタッチと、ネットワーク I/O 操作に使用できるソケットを作成できます。 WSK アプリケーションが呼び出すことでソケットを作成、 [ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)関数。 **WskSocket**関数で指し示されます、 **WskSocket**のメンバー、 [ **WSK\_プロバイダー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571175)添付ファイルの中に、WSK サブシステムによって返された構造体。

WSK ソケットのカテゴリを作成している新しいソケットが作成されるたびに WSK アプリケーションが指定する必要があります。 WSK ソケットのカテゴリの詳細については、次を参照してください。 [Winsock カーネル ソケット カテゴリ](winsock-kernel-socket-categories.md)します。

WSK アプリケーションにはアドレス ファミリ、ソケットの種類、およびプロトコルもを指定する必要がありますが、新しいソケットが作成されるたび。 WSK でサポートされているアドレス ファミリの詳細については、次を参照してください。 [WSK アドレス ファミリ](https://msdn.microsoft.com/library/windows/hardware/ff571151)します。

新しいソケットを作成するときに WSK アプリケーションは必要場合は、アプリケーションに、ソケットでイベントのコールバック関数が有効にするソケット コンテキストの値と、クライアント ディスパッチ テーブル構造へのポインターと提供する必要があります。 ソケットでのイベントのコールバック関数を有効にする方法の詳細については、次を参照してください。[の有効化と無効にするとイベントのコールバック関数](enabling-and-disabling-event-callback-functions.md)します。

ソケットが正常に作成された場合、 **IoStatus.Information** IRP のフィールドには、ソケット オブジェクトの構造体へのポインターが含まれています ( [ **WSK\_ソケット**](https://msdn.microsoft.com/library/windows/hardware/ff571182))新しいソケット。 Irp を WSK 関数を使用する方法の詳細については、次を参照してください。 [Winsock カーネル関数を使用して Irp](using-irps-with-winsock-kernel-functions.md)します。

次のコード例では、WSK アプリケーションがリスニング ソケットを作成する方法を示します。

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

接続指向のソケット WSK アプリケーションを呼び出すことができます、 [ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)関数を作成し、バインドして、1 つの関数の呼び出しでソケットを接続します。

 

 





