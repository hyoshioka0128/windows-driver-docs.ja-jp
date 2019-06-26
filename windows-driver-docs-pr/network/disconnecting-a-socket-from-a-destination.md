---
title: 宛先からのソケットの切断
description: 宛先からのソケットの切断
ms.assetid: 83755eb4-a24e-4fef-858d-d58318227dc0
keywords:
- Winsock カーネル WDK ネットワーク、切断しています
- WSK WDK ネットワーク、切断しています
- 確立されたソケット接続 WDK Winsock カーネル
- WDK Winsock Kernel の接続
- WDK Winsock Kernel の切断
- 変換先接続の WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82572ed424d9f3f1a9645f49689754591bf6cb14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386567"
---
# <a name="disconnecting-a-socket-from-a-destination"></a>宛先からのソケットの切断


Winsock カーネル (WSK) アプリケーションには、確立されたソケット接続経由でデータの送受信が完了したらは、接続指向のソケットが接続されているリモートのトランスポート アドレスから切断ができます。 WSK アプリケーションでは、リモートのトランスポート アドレスからソケットを切断を呼び出して、 [ **WskDisconnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect)関数。 WSK アプリケーションが実行するか、*中止になる切断*または*正常な切断*ソケットの。 中止になる切断と正常な切断の違いの詳細については、次を参照してください。 **WskDisconnect**します。

次のコード例では、どのように WSK アプリケーションを適切にから切断できます接続指向のソケット リモート トランスポート アドレスを示します。

```C++
// Prototype for the disconnect IoCompletion routine
NTSTATUS
  DisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to disconnect a socket from a remote transport address
NTSTATUS
  DisconnectSocket(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;
 
  // Get pointer to the socket's provider dispatch structure
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
    DisconnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the disconnect operation on the socket
  Status =
    Dispatch->WskDisconnect(
      Socket,
      NULL,  // No final data to be transmitted
      0,     // No flags (graceful disconnect)
      Irp
      );

  // Return the status of the call to WskDisconnect()
  return Status;
}

// Disconnect IoCompletion routine
NTSTATUS
  DisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the disconnect operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the socket object from the context
    Socket = (PWSK_SOCKET)Context;

    // Perform the next operation on the socket
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

WSK アプリケーションでは、ソケットの正常な切断を実行する場合、アプリケーションを送信するデータの最終的なバッファー リモート トランスポート アドレスへのポインターを渡すことによって、ソケットが切断されるまで、 [ **WSK\_BUF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_buf)構造体を[ **WskDisconnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect)関数。

WSK アプリケーションでは、接続されているリモートのトランスポート アドレスからソケットを接続したまま接続指向のソケットが閉じ、WSK サブシステムは自動的に中止になるソケットを閉じる前に、ソケットの切断を実行します。 ソケットを閉じることの詳細については、次を参照してください。[ソケットを閉じて](closing-a-socket.md)します。

 

 





