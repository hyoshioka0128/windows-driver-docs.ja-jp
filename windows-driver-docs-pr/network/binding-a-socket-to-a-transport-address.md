---
title: トランスポート アドレスへのソケットのバインド
description: トランスポート アドレスへのソケットのバインド
ms.assetid: b76bb601-536f-43de-b91c-932f4f08c274
keywords:
- Winsock カーネル WDK がネットワーク、ローカル トランスポート アドレス
- ネットワーク、WSK WDK ローカル トランスポート アドレス
- ソケット WDK Winsock Kernel のバインド
- ローカル トランスポート アドレス バインド WDK Winsock カーネル
- トランスポート アドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8426226782a66bb545bac440823549745e952e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354635"
---
# <a name="binding-a-socket-to-a-transport-address"></a>トランスポート アドレスへのソケットのバインド


Winsock カーネル (WSK) アプリケーションでは、ソケットが正常に作成、ローカル トランスポート アドレスにソケットをバインドできます。 着信接続を受け入れることができます、前に、ローカル トランスポート アドレスをリッスンしているソケットをバインドする必要があります。 データグラム ソケットは、送信、データグラムを受信する前に、ローカル トランスポート アドレスにバインドする必要があります。 接続指向のソケットは、リモートのトランスポート アドレスに接続する前に、ローカル トランスポート アドレスにバインドする必要があります。

**注**  ネットワーク データを送受信する基本的なソケットがサポートされません。 そのため、WSK アプリケーションでは、ローカル トランスポート アドレスに基本的なソケットをバインドすることはできません。

 

WSK アプリケーションでは、ローカル トランスポート アドレスにソケットをバインドを呼び出して、 [ **WskBind** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_bind)関数。 **WskBind**関数で指し示されます、 **WskBind**ソケットのプロバイダーのディスパッチ構造体のメンバー。 ソケットのプロバイダーのディスパッチ構造体を指す、**ディスパッチ**ソケット オブジェクトの構造体のメンバー ( [ **WSK\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_socket)) によって返された、ソケットの作成時に WSK サブシステムです。

ソケットは、ローカルのワイルドカード アドレスにバインドできます。 ローカルのワイルドカード アドレスにバインドされたソケットの動作に関する詳細については、次を参照してください。 **WskBind**します。

次のコード例では、ローカル トランスポート アドレスを WSK アプリケーションがリスニング ソケットをバインドする方法を示します。

```C++
// Prototype for the bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to bind a listening socket to a local transport address
NTSTATUS
  BindListeningSocket(
    PWSK_SOCKET Socket,
    PSOCKADDR LocalAddress
    )
{
  PWSK_PROVIDER_LISTEN_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_LISTEN_DISPATCH)(Socket->Dispatch);

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
    BindComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the bind operation on the socket
  Status =
    Dispatch->WskBind(
      Socket,
      LocalAddress,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskBind()
  return Status;
}

// Bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the bind operation
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

接続指向のソケット WSK アプリケーションを呼び出すことができます、 [ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)関数を作成し、バインドして、1 つの関数の呼び出しでソケットを接続します。

 

 





