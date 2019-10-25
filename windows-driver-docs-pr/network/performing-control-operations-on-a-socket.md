---
title: ソケットの制御操作の実行
description: ソケットの制御操作の実行
ms.assetid: 5d6ff02a-dc50-4818-9d0d-ba741fe7dfd8
keywords:
- Winsock カーネル WDK ネットワーク、制御操作
- WSK WDK ネットワーク、制御操作
- コントロール操作 WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f64863a2ace8c4dac3859222a08e2ce6a17215
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843687"
---
# <a name="performing-control-operations-on-a-socket"></a>ソケットの制御操作の実行


Winsock カーネル (WSK) アプリケーションでソケットが正常に作成されたら、ソケットに対して制御操作を実行できます。 ソケットに対して実行できる制御操作には、ソケットオプションの設定と取得、ソケットの IOCTL 操作の実行などがあります。

WSK アプリケーションは、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出すことによって、ソケットに対する制御操作を実行します。 **Wskcontrolsocket**関数は、ソケットのプロバイダーディスパッチ構造体の**wskcontrolsocket**メンバーによってポイントされています。 ソケットの作成時に WSK サブシステムによって返されたソケットオブジェクト構造 ( [**wsk\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)) の**ディスパッチ**メンバーによって、ソケットのプロバイダーディスパッチ構造体がポイントされます。

次のコード例では、WSK アプリケーションで、データグラムソケットに対して[**SO\_EXCLUSIVEADDRUSE**](https://docs.microsoft.com/windows-hardware/drivers/network/so-exclusiveaddruse) socket オプションを設定する方法を示します。

```C++
// Prototype for the control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to set the SO_EXCLUSIVEADDRUSE socket option
// on a datagram socket
NTSTATUS
  SetExclusiveAddrUse(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  ULONG SocketOptionState;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
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
    ControlSocketComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Set the socket option state to 1 to set the socket option
  SocketOptionState = 1;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_EXCLUSIVEADDRUSE,
      SOL_SOCKET,
      sizeof(ULONG),
      &SocketOptionState,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the control operation
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

サポートされている各ソケットオプションの詳細については、「 [**Wsk Socket options**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-socket-options)」を参照してください。

次のコード例では、WSK アプリケーションで、データグラムソケットに対するリモート\_アドレスソケットの IOCTL 操作\_設定された[**SIO\_wsk\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-set-remote-address)実行する方法を示します。

```C++
// Prototype for the control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to perform the SIO_WSK_SET_REMOTE_ADDRESS socket
// IOCTL operation on a datagram socket
NTSTATUS
  SetRemoteAddress(
    PWSK_SOCKET Socket,
    PSOCKADDR RemoteAddress
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
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
    ControlSocketComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the IOCTL operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskIoctl,
 SIO_WSK_SET_REMOTE_ADDRESS,
      0,
      sizeof(SOCKADDR_IN),  // AF_INET
      RemoteAddress,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the control operation
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

サポートされている各ソケット IOCTL 操作の詳細については、「 [Wsk ソケット Ioctl 操作](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-socket-ioctl-operations)」を参照してください。

 

 





