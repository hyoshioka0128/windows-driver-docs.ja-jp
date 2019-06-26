---
title: データグラム ソケット経由でのデータの受信
description: データグラム ソケット経由でのデータの受信
ms.assetid: 650b7688-967e-4ce6-80ad-8f7b6e1ec009
keywords:
- データグラムの受信
- データグラム ソケット WDK Winsock カーネル
- WskReceiveFrom
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96a47bd3ac477a57cf85e24665c9979945f0f95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353294"
---
# <a name="receiving-data-over-a-datagram-socket"></a>データグラム ソケット経由でのデータの受信


Winsock カーネル (WSK) アプリケーションがローカル トランスポート アドレスにデータグラム ソケットをバインドした後、ソケットを使ってデータグラムを受信できます。 WSK アプリケーション データグラム ソケット経由で呼び出すことによって、データグラムを受信する、 [ **WskReceiveFrom** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from)関数。

次のコード例では、データグラム ソケット経由で、WSK アプリケーションがデータグラムを受信する方法を示します。

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

呼び出す代わりとして、 [ **WskReceiveFrom** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from)データグラム ソケット経由で各データグラムを受信する関数を WSK アプリケーションを有効にすることができます、 [ *WskReceiveFromEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event)ソケットでのイベントのコールバック関数。 WSK アプリケーションを使用する場合、 *WskReceiveFromEvent*データグラム ソケットでのイベントのコールバック関数、WSK サブシステムを呼び出す、ソケットの*WskReceiveFromEvent*たびに新しいイベントのコールバック関数データグラムは、ソケットで受信されます。 データグラム ソケットの有効化の詳細については*WskReceiveFromEvent*イベントのコールバック関数を参照してください[の有効化と無効にするとイベントのコールバック関数](enabling-and-disabling-event-callback-functions.md)します。

コード例を次に示す方法 WSK アプリケーションで受信できますデータグラム WSK サブシステム データグラム ソケットを呼び出すことによって*WskReceiveFromEvent*イベント コールバック関数。

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

データグラム ソケットの場合[ *WskReceiveFromEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event)イベント コールバック関数は取得できません、データグラムのすべての一覧から[ **WSK\_データグラム\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_datagram_indication)によって示される構造体、 *DataIndication*パラメーターの状態を返すことによってさらに処理するためのリストを保持して\_保留します。 このような状況で WSK アプリケーションを呼び出す必要があります、 [ **WskRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff571144(v=vs.85))関数解放 WSK の一覧を\_データグラム\_を示す値構造体にバックアップした後、WSK サブシステムこれには、データグラムのすべてを一覧内の構造体から取得が完了しました。

 

 





