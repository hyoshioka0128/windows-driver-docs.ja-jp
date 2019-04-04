---
title: データグラム ソケット経由でのデータの送信
description: データグラム ソケット経由でのデータの送信
ms.assetid: 5748ac2a-177f-4fe9-a55b-85eec45d5afa
keywords:
- データグラムを送信します。
- データグラム ソケット WDK Winsock カーネル
- WskSendTo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d5848cf1a2abcf49e9ce5d373058d48a3b8efdb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580728"
---
# <a name="sending-data-over-a-datagram-socket"></a>データグラム ソケット経由でのデータの送信


Winsock カーネル (WSK) アプリケーションがローカル トランスポート アドレスにデータグラム ソケットをバインドした後、ソケットを使ってデータグラムを送信できます。 WSK アプリケーション データグラム ソケット経由で呼び出すことによって、データグラムを送信する、 [ **WskSendTo** ](https://msdn.microsoft.com/library/windows/hardware/ff571148)関数。

次のコード例では、データグラム ソケット経由で、WSK アプリケーションがデータグラムを送信する方法を示します。

```C++
// Prototype for the send datagram IoCompletion routine
NTSTATUS
  SendDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to send a datagram
NTSTATUS
  SendDatagram(
    PWSK_SOCKET Socket,
    PWSK_BUF DatagramBuffer,
    PSOCKADDR RemoteAddress
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_DATAGRAM_DISPATCH)(Socket->Dispatch);

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
    SendDatagramComplete,
    DatagramBuffer,  // Use the datagram buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the send operation on the socket
  Status =
    Dispatch->WskSendTo(
      Socket,
      DatagramBuffer,
      0,  // No flags
      RemoteAddress,
      0,
      NULL,  // No associated control info
      Irp
      );

  // Return the status of the call to WskSendTo()
  return Status;
}

// Send datagram IoCompletion routine
NTSTATUS
  SendDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DatagramBuffer;
  ULONG ByteCount;

  // Check the result of the send operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the datagram buffer
    DatagramBuffer = (PWSK_BUF)Context;

    // Get the number of bytes sent
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Re-use or free the datagram buffer
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

WSK アプリケーションがリモートの固定のトランスポート アドレスまたはデータグラム ソケットの固定の送信先のトランスポート アドレスのいずれかを設定する場合、 *RemoteAddress*に渡されるパラメーター、 [ **WskSendTo**](https://msdn.microsoft.com/library/windows/hardware/ff571148)関数は省略可能でありできる**NULL**します。 場合**NULL**データグラムをリモートの固定のトランスポート アドレスまたは固定の送信先のトランスポート アドレスに送信します。 場合以外**NULL**データグラムをリモートの指定したトランスポート アドレスに送信します。

データグラム ソケットに対して固定のリモート トランスポート アドレスを設定する方法についての詳細については、[ **SIO\_WSK\_設定\_リモート\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff570820)を参照してください。

データグラム ソケットに対して固定の送信先のトランスポート アドレスを設定する方法についての詳細については、次を参照してください[ **SIO\_WSK\_設定\_SENDTO\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff570821).

 

 





