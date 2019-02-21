---
title: 接続指向のソケット経由でデータを受信
description: 接続指向のソケット経由でデータを受信
ms.assetid: 189fa236-25d6-4eea-ad77-df76363576db
keywords:
- 接続指向のソケット WDK Winsock カーネル
- WskReceive
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bca3dbc90a94471ba9e6c6018ae11e6292b5823f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527979"
---
# <a name="receiving-data-over-a-connection-oriented-socket"></a>接続指向のソケット経由でデータを受信


Winsock カーネル (WSK) アプリケーションがリモートのトランスポート アドレスに接続指向のソケットを接続した後、ソケットを使ってデータを受信できます。 WSK アプリケーションでは、リッスン ソケットの受け入れ、接続指向のソケットでもデータを受信できます。 WSK アプリケーション接続指向のソケット経由で呼び出すことによってデータを受信する、 [ **WskReceive** ](https://msdn.microsoft.com/library/windows/hardware/ff571139)関数。

次のコード例では、WSK アプリケーションが接続指向のソケット経由でデータを受信する方法を示します。

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

呼び出す代わりとして、 [ **WskReceive** ](https://msdn.microsoft.com/library/windows/hardware/ff571139)接続指向のソケット経由でデータを受信する関数を WSK アプリケーションを有効にすることができます、 [ *WskReceiveEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571140)ソケットでのイベントのコールバック関数。 WSK アプリケーションを使用する場合、 *WskReceiveEvent*接続指向のソケットでのイベントのコールバック関数、WSK サブシステムを呼び出す、ソケットの*WskReceiveEvent*イベント コールバック関数のたびに新しいデータは、ソケットで受信されます。 接続指向のソケットの有効化の詳細については*WskReceiveEvent*イベントのコールバック関数を参照してください[の有効化と無効にするとイベントのコールバック関数](enabling-and-disabling-event-callback-functions.md)します。

次のコード例は、接続指向のソケットの呼び出す WSK サブシステムによって、WSK アプリケーションがデータを受信する方法を示しています。 *WskReceiveEvent*イベント コールバック関数。

```C++
// A connection-oriented socket&#39;s WskReceiveEvent
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

接続指向のソケットの場合、 [ *WskReceiveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571140)イベント コールバック関数はのすべてのリストに含まれるデータを取得できません[ **WSK\_データ\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff571165)によって示される構造体、 *DataIndication*パラメーターの状態を返すことによってさらに処理するためのリストを保持して\_保留します。 このような状況で WSK アプリケーションを呼び出す必要があります、 [ **WskRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff571144)関数解放 WSK の一覧を\_データ\_を示す値構造体を WSK サブシステムにバックアップした後リスト内の構造体から取得するすべてのデータを完了します。

接続指向のソケットの場合、 *WskReceiveEvent*イベント コールバック関数は受信したデータのバイト数の合計の一部のみを受け入れるが指す変数を設定する必要があります、 *BytesAccepted*パラメーターを実際に許可されたデータのバイト数。 ただし場合、ソケットの*WskReceiveEvent*イベント コールバック関数が受け入れるすべての受信データを指す変数を設定する必要はありません、 *BytesAccepted*パラメーター。

 

 





