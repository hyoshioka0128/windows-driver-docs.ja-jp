---
title: Winsock カーネル関数での IRP の使用
description: Winsock カーネル関数での IRP の使用
ms.assetid: eb7af09c-2312-4127-a0dc-324b208c1455
keywords:
- Winsock カーネル WDK ネットワー キング、Irp
- ネットワーク、WSK WDK Irp
- Irp WDK Winsock カーネル
- WDK Winsock Kernel 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73df49f09fa5f74d24afe806d43665cf960df4ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569641"
---
# <a name="using-irps-with-winsock-kernel-functions"></a>Winsock カーネル関数での IRP の使用


Winsock カーネル (WSK)[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)ネットワーク I/O 操作の非同期完了の Irp を使用します。 各 WSK 関数では、パラメーターとして、ポインターが IRP を受け取ります。 WSK 関数によって実行される操作が完了したら、WSK サブシステムは IRP を完了します。

IRP WSK 関数に渡す WSK アプリケーションを使用するは、次の方法のいずれかで取得できます。

-   WSK アプリケーションが呼び出すことによって、IRP を割り当てます、 [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)関数。 このような状況で WSK アプリケーションは、I/O スタックの少なくとも 1 つの場所で IRP を割り当てる必要があります。

-   WSK アプリケーションには、以前の割り当てを完了した IRP が再利用されます。 このような状況で、WSK を呼び出す必要があります、 [ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661) IRP を再初期化する関数。

-   WSK アプリケーションより高いレベルのドライバーまたは I/O マネージャーのいずれかを渡された IRP を使用します。 このような状況で IRP が WSK サブシステムによって少なくとも 1 つ残り I/O スタックの場所用に使用できるが必要です。

WSK アプリケーションが使用する IRP、WSK を呼び出すために機能、設定できる、 [ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354) WSK サブシステムによって IRP が完了したときに呼び出される IRP のルーチンです。 WSK アプリケーション設定、 **IoCompletion**呼び出して IRP の日常的な[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)関数。 IRP が発生した方法に応じて、 **IoCompletion**ルーチンは、必須またはオプションのいずれか。

-   WSK アプリケーション、IRP を割り当てまたは以前に割り当てられた後に設定する必要がある IRP を再利用する場合、 **IoCompletion** WSK 関数を呼び出す前に IRP のルーチンです。 このような状況で WSK アプリケーションを指定する必要があります**TRUE**の*InvokeOnSuccess*、 *InvokeOnError*、および*InvokeOnCancel*パラメーターに渡される、 **IoSetCompletionRoutine**ことを確認する関数、 **IoCompletion**ルーチンが常に呼び出されます。 さらに、 **IoCompletion** IRP が状態を返す必要があります常にに対して設定されているルーチン\_詳細\_処理\_IRP の完了処理を終了するには、必要な作業です。 WSK アプリケーションを実行する場合の後の IRP を使用して、 **IoCompletion**ルーチンが呼び出されると、その後に呼び出す必要があります、 [ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)を解放する前に IRP 関数返す、 **IoCompletion**ルーチン。 WSK アプリケーションは IRP を確保できない場合は、別の WSK 関数の呼び出しの IRP 再利用ができます。

-   WSK アプリケーションより高いレベルのドライバーまたは I/O マネージャーに渡された IRP を使用する場合に設定する必要があります、 **IoCompletion**その必要がある場合にのみ、WSK 関数を呼び出す前に IRP の日常的な通知を受け取るときに、操作実行、WSK によって関数が完了します。 WSK アプリケーションが設定されていない場合、 **IoCompletion** IRP の日常的な IRP が完了したときに IRP が渡すことがより高いレベルのドライバーへのバックアップまたは IRP の完了の通常の処理に従って I/O マネージャーにします。 WSK アプリケーションが設定されている場合、 **IoCompletion** 、IRP の日常的な**IoCompletion**ルーチンが状態を返せるか\_成功または状態\_詳細\_処理\_必要な作業です。 場合、 **IoCompletion**ルーチンがステータスを返します\_成功すると、IRP の完了処理は、通常どおり続行されます。 場合、 **IoCompletion**ルーチンがステータスを返します\_詳細\_処理\_必要に応じて、WSK アプリケーションする必要があります、IRP 呼び出して完了[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) WSK 関数によって実行された操作の結果の処理が完了した後。 WSK アプリケーションより高いレベルのドライバーまたは I/O マネージャーに渡された IRP が解放しない必要があります。

**注**  WSK アプリケーションが設定されている場合、 **IoCompletion**より高いレベルのドライバーをするか、I/O マネージャーをして渡された IRP の日常的な**IoCompletion**ルーチンを確認する必要があります、 **PendingReturned** IRP と呼び出しのメンバー、 [ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)関数の場合、 **PendingReturned**メンバーが**TRUE**します。 詳細については、[、IoCompletion ルーチンを実装する](https://msdn.microsoft.com/library/windows/hardware/ff547084)を参照してください。

 

WSK アプリケーション設定以外 WSK 関数に渡される Irp を初期化しません、 **IoCompletion**ルーチン。 WSK アプリケーションでは、WSK 関数に IRP が成功したとき、WSK サブシステムは、アプリケーションに代わって、I/O スタック内の [次へ] の場所を設定します。

次のコード例では、WSK アプリケーションでの割り当ておよびソケットでの受信操作を実行するときに IRP の使用方法を示します。

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

場所、WSK アプリケーションでは、IRP を割り当てるし、完了ルーチンのによって解放、前の例に示すように、モデルは、WSK ドキュメントの残りの部分での例で使用されるモデルです。

次のコード例では、WSK アプリケーションが渡されたに高いレベルのドライバーまたは I/O マネージャーによって、ソケットでの受信操作を実行するときに IRP を使用する方法を示します。

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
    PWSK_BUF DataBuffer,
    PIRP Irp;  // IRP from a higher level driver or the I/O manager
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Set the completion routine for the IRP such that it is
  // only called if the receive operation succeeds.
  IoSetCompletionRoutine(
    Irp,
    ReceiveComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    FALSE,
    FALSE
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

  // Since the completion routine was only specified to
  // be called if the operation succeeds, this should
  // always be true.
  ASSERT(Irp->IoStatus.Status == STATUS_SUCCESS);

  // Check the pending status of the IRP
  if (Irp->PendingReturned == TRUE)
  {
    // Mark the IRP as pending
    IoMarkIrpPending(Irp);
  }

  // Get the pointer to the data buffer
  DataBuffer = (PWSK_BUF)Context;
 
  // Get the number of bytes received
  ByteCount = (ULONG)(Irp->IoStatus.Information);

  // Process the received data
  ...

  // Return STATUS_SUCCESS to continue the
  // completion processing of the IRP.
  return STATUS_SUCCESS;
}
```

Irp の使用に関する詳細については、[Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)を参照してください。

 

 





