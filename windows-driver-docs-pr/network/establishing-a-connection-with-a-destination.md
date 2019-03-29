---
title: 宛先との接続の確立
description: 宛先との接続の確立
ms.assetid: 1258ee32-3914-4832-b98b-361dace0abaf
keywords:
- Winsock カーネル WDK がネットワーク接続、リモートのトランスポート アドレス
- WSK WDK のネットワーク接続、リモートのトランスポート アドレス
- リモートのトランスポート アドレス バインド WDK Winsock カーネル
- トランスポート アドレス WDK Winsock カーネル
- 確立されたソケット接続 WDK Winsock カーネル
- WDK Winsock Kernel の接続
- 変換先接続の WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 389ed729c4c6d8376fca6b0a52cd37f159a17258
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349017"
---
# <a name="establishing-a-connection-with-a-destination"></a>宛先との接続の確立


Winsock カーネル (WSK) アプリケーションがローカル トランスポート アドレスに接続指向のソケットをバインドした後に、リモート システムとの接続を確立するために、ソケット、リモートのトランスポート アドレスを接続できます。 WSK アプリケーションは、送信したり、ソケット経由でデータを受信する前に、リモートのトランスポート アドレスに接続指向のソケットを接続する必要があります。

WSK アプリケーションでは、リモートのトランスポート アドレスにソケットを接続呼び出すことによって、 [ **WskConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571125)関数。 **WskConnect**関数で指し示されます、 **WskConnect**ソケットのプロバイダーのディスパッチ構造体のメンバー。 ソケットのプロバイダーのディスパッチ構造体を指す、**ディスパッチ**ソケット オブジェクトの構造体のメンバー ( [ **WSK\_ソケット**](https://msdn.microsoft.com/library/windows/hardware/ff571182)) によって返された、ソケットの作成時に WSK サブシステムです。

次のコード例では、リモートのトランスポート アドレスに、WSK アプリケーションが接続指向のソケットを接続する方法を示します。

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

WSK アプリケーションが呼び出すことができます、 [ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)関数を作成し、バインドして、1 つの関数の呼び出しで、接続指向のソケットを接続します。

 

 





