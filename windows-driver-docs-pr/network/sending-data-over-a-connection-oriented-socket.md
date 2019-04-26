---
title: 接続指向ソケット経由でのデータの送信
description: 接続指向ソケット経由でのデータの送信
ms.assetid: 290f3a8a-6bdc-4dd9-a9bf-4eede37bf1e5
keywords:
- 接続指向のソケット WDK Winsock カーネル
- WskSend
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e2c7616fae4e99526cd035c56366eed52f9cd6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346803"
---
# <a name="sending-data-over-a-connection-oriented-socket"></a>接続指向ソケット経由でのデータの送信


Winsock カーネル (WSK) アプリケーションがリモートのトランスポート アドレスに接続指向のソケットを接続した後、ソケットを使ってデータを送信できます。 WSK アプリケーションも、リッスン ソケットの受け入れ、接続指向のソケット経由でデータを送信できます。 WSK アプリケーション接続指向のソケット経由で呼び出すことによってデータを送信する、 [ **WskSend** ](https://msdn.microsoft.com/library/windows/hardware/ff571146)関数。

次のコード例では、WSK アプリケーションが接続指向のソケット経由でデータを送信する方法を示します。

```C++
// Prototype for the send IoCompletion routine
NTSTATUS
  SendComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to send data
NTSTATUS
  SendData(
    PWSK_SOCKET Socket,
    PWSK_BUF DataBuffer
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
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
    SendComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the send operation on the socket
  Status =
    Dispatch->WskSend(
      Socket,
      DataBuffer,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskSend()
  return Status;
}

// Send IoCompletion routine
NTSTATUS
  SendComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DataBuffer;
  ULONG ByteCount;

  // Check the result of the send operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the data buffer
    DataBuffer = (PWSK_BUF)Context;

    // Get the number of bytes sent
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Re-use or free the data buffer
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

 

 





