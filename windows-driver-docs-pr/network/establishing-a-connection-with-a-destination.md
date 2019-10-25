---
title: 宛先との接続の確立
description: 宛先との接続の確立
ms.assetid: 1258ee32-3914-4832-b98b-361dace0abaf
keywords:
- Winsock カーネル WDK ネットワーク、リモートトランスポートアドレス
- WSK WDK ネットワーク、リモートトランスポートアドレス
- リモートトランスポートアドレスバインド WDK Winsock カーネル
- トランスポートアドレス WDK Winsock カーネル
- 確立されたソケット接続 WDK Winsock カーネル
- 接続 WDK Winsock カーネル
- 宛先接続 WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ec07b3abebc92bdf45914a42de50605c39fa39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834771"
---
# <a name="establishing-a-connection-with-a-destination"></a>宛先との接続の確立


Winsock カーネル (WSK) アプリケーションは、接続指向のソケットをローカルトランスポートアドレスにバインドした後、リモートシステムとの接続を確立するために、ソケットをリモートトランスポートアドレスに接続できます。 WSK アプリケーションは、ソケット上でデータを送受信する前に、接続指向のソケットをリモートトランスポートアドレスに接続する必要があります。

WSK アプリケーションは、 [**Wskconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_connect)関数を呼び出して、ソケットをリモートトランスポートアドレスに接続します。 **Wskconnect**関数は、ソケットのプロバイダーディスパッチ構造体の**wskconnect**メンバーによってポイントされます。 ソケットの作成時に WSK サブシステムによって返されたソケットオブジェクト構造 ( [**wsk\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)) の**ディスパッチ**メンバーによって、ソケットのプロバイダーディスパッチ構造体がポイントされます。

次のコード例は、WSK アプリケーションが接続指向のソケットをリモートトランスポートアドレスに接続する方法を示しています。

```C++
// Prototype for the connect IoCompletion routine
NTSTATUS
  ConnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to connect a socket to a remote transport address
NTSTATUS
  ConnectSocket(
    PWSK_SOCKET Socket,
    PSOCKADDR RemoteAddress
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
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
    ConnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the connect operation on the socket
  Status =
    Dispatch->WskConnect(
      Socket,
      RemoteAddress,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskConnect()
  return Status;
}

// Connect IoCompletion routine
NTSTATUS
  ConnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the connect operation
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

WSK アプリケーションは、 [**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して、1つの関数呼び出しで接続指向のソケットを作成、バインド、および接続できます。

 

 





