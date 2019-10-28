---
title: データグラム ソケット経由でのデータの受信
description: データグラム ソケット経由でのデータの受信
ms.assetid: 650b7688-967e-4ce6-80ad-8f7b6e1ec009
keywords:
- 受信データグラム
- データグラムソケット WDK Winsock カーネル
- WskReceiveFrom
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a7f0ab3dfd8cc4760239a192b01091dec8e7200
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843468"
---
# <a name="receiving-data-over-a-datagram-socket"></a>データグラム ソケット経由でのデータの受信


Winsock カーネル (WSK) アプリケーションは、データグラムソケットをローカルトランスポートアドレスにバインドした後、ソケット上でデータグラムを受信できます。 WSK アプリケーションは、 [**WskReceiveFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from)関数を呼び出すことによって、データグラムソケットを介してデータグラムを受信します。

次のコード例は、WSK アプリケーションがデータグラムソケット経由でデータグラムを受信する方法を示しています。

```C++
// Prototype for the receive datagram IoCompletion routine
NTSTATUS
  ReceiveDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to receive a datagram
NTSTATUS
  ReceiveDatagram(
    PWSK_SOCKET Socket,
    PWSK_BUF DatagramBuffer
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
    ReceiveDatagramComplete,
    DatagramBuffer,  // Use the datagram buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the receive operation on the socket
  Status =
    Dispatch->WskReceiveFrom(
      Socket,
      DatagramBuffer,
      0,  // No flags are specified
      NULL,  // Not interested in the remote address
      NULL,  // Not interested in any associated control information
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskReceiveFrom()
  return Status;
}

// Receive datagram IoCompletion routine
NTSTATUS
  ReceiveDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DataBuffer;
  ULONG ByteCount;

  // Check the result of the receive operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the data buffer
    DataBuffer = (PWSK_BUF)Context;
 
    // Get the number of bytes received
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Process the received datagram
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

[**WskReceiveFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from)関数を呼び出してデータグラムソケット経由で各データグラムを受信する代わりに、wsk アプリケーションでは、ソケットで[*WskReceiveFromEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)イベントコールバック関数を有効にすることができます。 WSK アプリケーションで、データグラムソケットで*WskReceiveFromEvent*イベントコールバック関数が有効になっている場合、wsk サブシステムは、ソケットで新しいデータグラムを受信するたびに、ソケットの*WskReceiveFromEvent*イベントコールバック関数を呼び出します。 データグラムソケットの*WskReceiveFromEvent*イベントコールバック関数を有効にする方法の詳細については、「[イベントコールバック関数の有効化と無効化](enabling-and-disabling-event-callback-functions.md)」を参照してください。

次のコード例は、WSK アプリケーションが、データグラムソケットの*WskReceiveFromEvent*イベントコールバック関数を呼び出すことによって wsk サブシステムによってデータグラムを受信する方法を示しています。

```C++
// A datagram socket's WskReceiveFromEvent
// event callback function
NTSTATUS WSKAPI
  WskReceiveFromEvent(
    PVOID SocketContext,
    ULONG Flags,
    PWSK_DATAGRAM_INDICATION DataIndication
    )
{
  // Check for a valid data indication
  if (DataIndication != NULL)
  {
    // Loop through the list of data indication structures
    while (DataIndication != NULL)
    {
      // Process the data in the data indication structure
      ...

      // Move to the next data indication structure
      DataIndication = DataIndication->Next;
    }

    // Return status indicating the datagrams were received
    return STATUS_SUCCESS;
  }

  // Error
  else
  {
    // Close the socket
    ...

    // Return success since no datagrams were indicated
    return STATUS_SUCCESS;
  }
}
```

データグラムソケットの[*WskReceiveFromEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)イベントコールバック関数が、 *DataIndication*パラメーターによって示されている[ **\_\_の wsk**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_datagram_indication)のリストからすべてのデータグラムを取得していない場合は、ステータス\_PENDING を返すことで、さらに処理するためにリストを保持します。 このような状況では、WSK アプリケーションは[**Wskrelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff571144(v=vs.85))関数を呼び出して、wsk\_\_データグラムのリストを wsk サブシステムに解放する必要があります。これは、次の構造からすべてのデータグラムの取得が完了した後です。リスト。

 

 





