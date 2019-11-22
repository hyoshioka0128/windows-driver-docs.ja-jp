---
title: 宛先からのソケットの切断
description: 宛先からのソケットの切断
ms.assetid: 83755eb4-a24e-4fef-858d-d58318227dc0
keywords:
- Winsock カーネル WDK ネットワーク, 切断
- WSK WDK ネットワーク, 切断
- 確立されたソケット接続 WDK Winsock カーネル
- 接続 WDK Winsock カーネル
- WDK Winsock カーネルの切断
- 宛先接続 WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361908d2e31a633fd4436d09c1c874499b5ba04d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834885"
---
# <a name="disconnecting-a-socket-from-a-destination"></a>宛先からのソケットの切断


Winsock カーネル (WSK) アプリケーションが、確立されたソケット接続経由でのデータの送受信を終了した場合、接続先のリモートトランスポートアドレスから接続指向のソケットを切断できます。 WSK アプリケーションは、 [**Wskdisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect)関数を呼び出して、リモートトランスポートアドレスからソケットを切断します。 WSK アプリケーションは、中止*切断*またはソケットの*正常な切断*のいずれかを実行できます。 中止切断と正常な切断の違いの詳細については、「 **Wskdisconnect**」を参照してください。

次のコード例は、WSK アプリケーションがリモートトランスポートアドレスから接続指向ソケットを正常に切断する方法を示しています。

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

WSK アプリケーションがソケットの正常な切断を実行する場合、アプリケーションは[**wsk\_BUF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_buf)構造体へのポインターを[**wskdisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect)関数に渡すことによって、ソケットが切断される前に、データの最終的なバッファーをリモートトランスポートアドレスに送信できます。

WSK アプリケーションが、接続先のリモートトランスポートアドレスからソケットを最初に切断せずに接続指向ソケットを閉じた場合、WSK サブシステムはソケットを閉じる前に、ソケットの切断を自動的に実行します。 ソケットを閉じる方法の詳細については、「[ソケットを閉じる](closing-a-socket.md)」を参照してください。

 

 





