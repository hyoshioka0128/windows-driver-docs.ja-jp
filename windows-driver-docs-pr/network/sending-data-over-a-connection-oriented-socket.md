---
title: 接続指向ソケット経由でのデータの送信
description: 接続指向ソケット経由でのデータの送信
ms.assetid: 290f3a8a-6bdc-4dd9-a9bf-4eede37bf1e5
keywords:
- 接続指向のソケット WDK Winsock カーネル
- WskSend
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c63ec7780ff4c31489c50b20e229750eafaaa410
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378646"
---
# <a name="sending-data-over-a-connection-oriented-socket"></a>接続指向ソケット経由でのデータの送信


Winsock カーネル (WSK) アプリケーションがリモートのトランスポート アドレスに接続指向のソケットを接続した後、ソケットを使ってデータを送信できます。 WSK アプリケーションも、リッスン ソケットの受け入れ、接続指向のソケット経由でデータを送信できます。 WSK アプリケーション接続指向のソケット経由で呼び出すことによってデータを送信する、 [ **WskSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send)関数。

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

 

 





