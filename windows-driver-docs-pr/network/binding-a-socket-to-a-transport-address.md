---
title: トランスポート アドレスへのソケットのバインド
description: トランスポート アドレスへのソケットのバインド
ms.assetid: b76bb601-536f-43de-b91c-932f4f08c274
keywords:
- Winsock カーネル WDK ネットワーク、ローカルトランスポートアドレス
- WSK WDK ネットワーク、ローカルトランスポートアドレス
- バインドソケット WDK Winsock カーネル
- ローカルトランスポートアドレスバインド WDK Winsock カーネル
- トランスポートアドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f29c8b98e24064fa3e3aad3f8364e62ac33947db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838221"
---
# <a name="binding-a-socket-to-a-transport-address"></a>トランスポート アドレスへのソケットのバインド


Winsock カーネル (WSK) アプリケーションでソケットが正常に作成された後、そのソケットをローカルトランスポートアドレスにバインドできます。 リッスンソケットは、受信接続を受け入れる前に、ローカルトランスポートアドレスにバインドされている必要があります。 データグラムを送信または受信するには、データグラムソケットがローカルトランスポートアドレスにバインドされている必要があります。 リモートトランスポートアドレスに接続するには、接続指向のソケットがローカルトランスポートアドレスにバインドされている必要があります。

**注**  基本ソケットは、ネットワークデータの送受信をサポートしていません。 そのため、WSK アプリケーションでは、基本ソケットをローカルトランスポートアドレスにバインドすることはできません。

 

WSK アプリケーションは、 [**Wskbind**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_bind)関数を呼び出して、ソケットをローカルトランスポートアドレスにバインドします。 **Wskbind**関数は、ソケットのプロバイダーディスパッチ構造体の**wskbind**メンバーによってポイントされます。 ソケットの作成時に WSK サブシステムによって返されたソケットオブジェクト構造 ( [**wsk\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)) の**ディスパッチ**メンバーによって、ソケットのプロバイダーディスパッチ構造体がポイントされます。

ソケットは、ローカルのワイルドカードアドレスにバインドできます。 ローカルのワイルドカードアドレスにバインドされているソケットの動作の詳細については、「 **Wskbind**」を参照してください。

次のコード例は、WSK アプリケーションがリッスンソケットをローカルトランスポートアドレスにバインドする方法を示しています。

```C++
// Prototype for the bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to bind a listening socket to a local transport address
NTSTATUS
  BindListeningSocket(
    PWSK_SOCKET Socket,
    PSOCKADDR LocalAddress
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
    BindComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the bind operation on the socket
  Status =
    Dispatch->WskBind(
      Socket,
      LocalAddress,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskBind()
  return Status;
}

// Bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the bind operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
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

接続指向のソケットの場合、WSK アプリケーションは[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して、1つの関数呼び出しでソケットを作成、バインド、および接続することができます。

 

 





