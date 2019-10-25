---
title: データグラム ソケット経由でのデータの送信
description: データグラム ソケット経由でのデータの送信
ms.assetid: 5748ac2a-177f-4fe9-a55b-85eec45d5afa
keywords:
- 送信 (データグラムを)
- データグラムソケット WDK Winsock カーネル
- WskSendTo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d2fca60c9f45739aaaf1c678bf04b27eee863b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841968"
---
# <a name="sending-data-over-a-datagram-socket"></a>データグラム ソケット経由でのデータの送信


Winsock カーネル (WSK) アプリケーションは、データグラムソケットをローカルトランスポートアドレスにバインドした後、ソケットを介してデータグラムを送信できます。 WSK アプリケーションは、 [**Wsksendto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)関数を呼び出してデータグラムソケットを介してデータグラムを送信します。

次のコード例は、WSK アプリケーションがデータグラムソケットを介してデータグラムを送信する方法を示しています。

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

WSK アプリケーションで、データグラムソケットに対して固定のリモートトランスポートアドレスまたは固定の送信先トランスポートアドレスのいずれかが設定されている場合、 [**Wsksendto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)関数に渡される*remoteaddress*パラメーターは省略可能であり、 **NULL**にすることができます。 **NULL**の場合、データグラムは固定されたリモートトランスポートアドレスまたは固定の送信先トランスポートアドレスに送信されます。 **NULL**以外の場合は、指定されたリモートトランスポートアドレスにデータグラムが送信されます。

データグラムソケットの固定リモートトランスポートアドレスの設定の詳細については、「 [**SIO\_WSK\_SET\_remote\_address**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-set-remote-address)」を参照してください。

データグラムソケットの固定送信先トランスポートアドレスの設定の詳細については、「 [**SIO\_WSK\_SET\_SENDTO\_address**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-set-sendto-address)」を参照してください。

 

 





