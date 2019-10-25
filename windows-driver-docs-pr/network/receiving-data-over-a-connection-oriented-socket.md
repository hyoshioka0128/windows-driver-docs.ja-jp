---
title: 接続指向ソケット経由でのデータの受信
description: 接続指向ソケット経由でのデータの受信
ms.assetid: 189fa236-25d6-4eea-ad77-df76363576db
keywords:
- 接続指向ソケット WDK Winsock カーネル
- WskReceive
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14f4d6c95e2b73a1e436663a34226e44791501d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844847"
---
# <a name="receiving-data-over-a-connection-oriented-socket"></a>接続指向ソケット経由でのデータの受信


Winsock カーネル (WSK) アプリケーションは、接続指向のソケットをリモートトランスポートアドレスに接続した後、ソケット経由でデータを受信できます。 WSK アプリケーションは、リッスンしているソケットで受け入れられた接続指向のソケットを介してデータを受信することもできます。 WSK アプリケーションは、 [**Wskreceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)関数を呼び出すことにより、接続指向のソケットを介してデータを受信します。

次のコード例は、WSK アプリケーションが接続指向のソケットを介してデータを受信する方法を示しています。

```C++
// Prototype for the receive IoCompletion routine
NTSTATUS
  ReceiveComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to receive data
NTSTATUS
  ReceiveData(
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
    ReceiveComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the receive operation on the socket
  Status =
    Dispatch->WskReceive(
      Socket,
      DataBuffer,
      0,  // No flags are specified
      Irp
      );

  // Return the status of the call to WskReceive()
  return Status;
}

// Receive IoCompletion routine
NTSTATUS
  ReceiveComplete(
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

    // Process the received data
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

接続指向のソケットを介してデータを受信するために[**Wskreceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)関数を呼び出す代わりに、wsk アプリケーションでは、そのソケットで[*wskreceiveevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)イベントコールバック関数を有効にすることができます。 WSK アプリケーションで、接続指向のソケットで*Wskreceiveevent*イベントコールバック関数が有効になっている場合、wsk サブシステムは、新しいデータがソケットで受信されるたびに、*そのイベントコール*バック関数を呼び出します。 接続指向ソケットの*Wskreceiveevent*イベントコールバック関数を有効にする方法の詳細については、「[イベントコールバック関数の有効化と無効化](enabling-and-disabling-event-callback-functions.md)」を参照してください。

次のコード例は、WSK アプリケーションが、接続指向のソケットの*Wskreceiveevent*イベントコールバック関数を呼び出す wsk サブシステムによってデータを受信する方法を示しています。

```C++
// A connection-oriented socket's WskReceiveEvent
// event callback function
NTSTATUS WSKAPI
  WskReceiveEvent(
    PVOID SocketContext,
    ULONG Flags,
    PWSK_DATA_INDICATION DataIndication,
    SIZE_T BytesIndicated,
    SIZE_T *BytesAccepted
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

    // Return status indicating the data was received
    return STATUS_SUCCESS;
  }

  // Error
  else
  {
    // Close the socket
    ...

    // Return success since no data was indicated
    return STATUS_SUCCESS;
  }
}
```

接続指向のソケットの[*Wskreceiveevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)イベントコールバック関数が、 *DataIndication*パラメーターによって示された[**wsk\_データ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_data_indication)表示構造体の一覧に含まれるすべてのデータを取得しない場合、ステータス\_PENDING を返すことで、さらに処理するためにリストを保持できます。 このような状況では、WSK アプリケーションは[**Wskrelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff571144(v=vs.85))関数を呼び出す必要があります。この関数は、リスト内の構造からすべてのデータの取得を完了した後、wsk\_データ\_表示構造体のリストを wsk サブシステムに戻します。

接続指向のソケットの*Wskreceiveevent*イベントコールバック関数が、受信したデータの合計バイト数の部分のみを受け入れる場合は、 *bytesaccepted*パラメーターが指す変数を、データのバイト数に設定する必要があります。は実際に受け入れられました。 ただし、ソケットの*Wskreceiveevent*イベントコールバック関数が受信したすべてのデータを受け入れる場合は、 *bytesaccepted*パラメーターが指す変数を設定する必要はありません。

 

 





