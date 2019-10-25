---
title: Winsock カーネル関数での IRP の使用
description: Winsock カーネル関数での IRP の使用
ms.assetid: eb7af09c-2312-4127-a0dc-324b208c1455
keywords:
- Winsock カーネル WDK ネットワーク、Irp
- WSK WDK ネットワーク、Irp
- Irp WDK Winsock カーネル
- functions WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47ebaecaf7d4d476dbf6fcd88fed531cb0872104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842991"
---
# <a name="using-irps-with-winsock-kernel-functions"></a>Winsock カーネル関数での IRP の使用


Winsock カーネル (WSK)[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)では、ネットワーク i/o 操作の非同期完了に irp を使用します。 各 WSK 関数は、パラメーターとして IRP へのポインターを受け取ります。 Wsk サブシステムは、WSK 関数によって実行された操作が完了した後に、IRP を完了します。

Wsk アプリケーションが WSK 関数に渡すために使用する IRP は、次のいずれかの方法で発生する可能性があります。

-   WSK アプリケーションは、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)関数を呼び出すことによって、IRP を割り当てます。 このような状況では、WSK アプリケーションは、少なくとも1つの i/o スタックの場所で IRP を割り当てる必要があります。

-   WSK アプリケーションは、以前に割り当てた完了した IRP を再利用します。 このような状況では、WSK は[**IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)関数を呼び出して、IRP を再初期化する必要があります。

-   WSK アプリケーションは、上位レベルのドライバーまたは i/o マネージャーによって渡された IRP を使用します。 このような状況では、IRP は WSK サブシステムが使用できるように、残りの1つ以上の i/o スタック位置を少なくとも1つ持つ必要があります。

Wsk アプリケーションに WSK 関数の呼び出しに使用する IRP があると、WSK サブシステムが IRP を完了するときに、irp が呼び出されるように[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できます。 WSK アプリケーションは、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)関数を呼び出すことによって、IRP の**iocompletion**ルーチンを設定します。 IRP の発生方法によっては、 **Iocompletion**ルーチンが必要になるか、または省略可能になります。

-   WSK アプリケーションが IRP を割り当てた場合、または以前に割り当てた IRP を再利用している場合は、WSK 関数を呼び出す前に、IRP の**Iocompletion**ルーチンを設定する必要があります。 このような状況では、WSK アプリケーションは、 **IosetInvokeOnSuccess ルーチン**関数に渡される InvokeOnCancel パラメーター、 *invokeonerror*パラメーター、およびパラメーターに**TRUE**を指定して、 **IoCompletion**ルーチンは常に呼び出されます。 さらに、irp に対して設定されている**iocompletion**ルーチンは、irp の完了処理を終了するために必要な\_処理\_の状態\_常に返す必要があります。 IOCOMPLETION アプリケーションが、 **iocompletion**ルーチンが呼び出された後に irp を使用して実行された場合は、 **iocompletion**ルーチンから戻る前に、 [**iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)関数を呼び出して irp を解放する必要があります。 WSK アプリケーションで IRP が解放されない場合は、別の WSK 関数の呼び出しに対して IRP を再利用できます。

-   WSK アプリケーションで、上位レベルのドライバーまたは i/o マネージャーによって渡された IRP が使用されている場合、wsk 関数を呼び出す前に、wsk 関数を呼び出す前に、その IRP の**Iocompletion**ルーチンを設定する必要があります。が完了しました。 WSK アプリケーションが IRP の**Iocompletion**ルーチンを設定していない場合、irp が完了すると、irp は、通常の irp 完了処理に従って、上位レベルのドライバーまたは i/o マネージャーに戻されます。 WSK アプリケーションで IRP の**Iocompletion**ルーチンが設定されている場合、 **iocompletion**ルーチンは、必要な\_処理\_\_の状態\_成功または状態のどちらかを返すことができます。 **Iocompletion**ルーチンが STATUS\_SUCCESS を返した場合、IRP の完了処理は通常どおり続行されます。 **Iocompletion**ルーチンが、必要な\_処理\_よりも多くの状態\_返す場合、wsk アプリケーションは、の操作結果の処理が完了した後に[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すことによって IRP を完了する必要があります。WSK 関数によって実行されます。 WSK アプリケーションは、上位レベルのドライバーまたは i/o マネージャーによって渡された IRP を解放しないでください。

**  ** wsk アプリケーションが、上位レベルのドライバーまたは i/o マネージャーによって渡された IRP に対して**iocompletion**ルーチンを設定した場合、 **iocompletion**ルーチンは、次のいずれかの**pendingreturned**たメンバーを確認する必要があります。**Pendingreturned よって返される**メンバーが**TRUE**の場合、IRP は[**iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)関数を呼び出します。 詳細については、「 [IoCompletion ルーチンの実装](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-an-iocompletion-routine)」を参照してください。

 

WSK アプリケーションは、Iocompletion 関数に渡される Irp を、 **Iocompletion**ルーチンを設定する以外に初期化しません。 Wsk アプリケーションから WSK 関数に IRP が渡されると、WSK サブシステムによって、アプリケーションの代わりに次の i/o スタック位置が設定されます。

次のコード例は、WSK アプリケーションで、ソケットに対して受信操作を実行するときに、IRP を割り当てて使用する方法を示しています。

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

前の例で示したモデルでは、WSK アプリケーションが IRP を割り当て、それを完了ルーチンで解放しています。このモデルは、WSK ドキュメントの残りの部分を通じて、例で使用されるモデルです。

次のコード例では、WSK アプリケーションで、上位レベルのドライバーによって渡された IRP、またはソケットで受信操作を実行するときに i/o マネージャーが使用する方法を示します。

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

Irp の使用方法の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。

 

 





