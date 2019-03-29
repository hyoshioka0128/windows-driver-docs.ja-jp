---
title: 拡張インターフェイスの登録
description: 拡張インターフェイスの登録
ms.assetid: 33dc32da-9bc1-40b4-8737-ec132ec36708
keywords:
- Winsock カーネル WDK がネットワーク接続、拡張機能インターフェイス
- WSK WDK のネットワーク接続、拡張機能インターフェイス
- 拡張機能インターフェイス WDK Winsock カーネル
- Winsock Kernel 拡張機能インターフェイスを登録します。
- SIO_WSK_REGISTER_EXTENSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8c178bb02314640a9b9db5d0922ee27289c4a9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348635"
---
# <a name="registering-an-extension-interface"></a>拡張インターフェイスの登録


1 つ以上のソケットを登録するは、Winsock カーネル (WSK) アプリケーションでは、ソケットが正常に作成、[拡張機能インターフェイス](winsock-kernel-extension-interfaces.md)WSK サブシステムでサポートされています。 WSK アプリケーションの決定を調べることで、WSK サブシステムによって拡張機能インターフェイスのセットがサポートされている、**バージョン**のメンバー、 [ **WSK\_プロバイダー\_ディスパッチ** ](https://msdn.microsoft.com/library/windows/hardware/ff571175) WSK サブシステムは、添付ファイルの中に、アプリケーションに返される構造体。

各拡張機能インターフェイスは、WSK NPI から独立している、NPI によって定義されます。 ただし、拡張機能インターフェイスの NPIs が NPI 固有の特性をサポートしていないことに注意してください。

WSK アプリケーションを実行することによって拡張機能インターフェイスの登録、 [ **SIO\_WSK\_登録\_拡張子**](https://msdn.microsoft.com/library/windows/hardware/ff570819)ソケット、ソケットの IOCTL 操作。 ソケットの IOCTL 操作を実行する方法の詳細については、次を参照してください。[ソケットで管理操作を実行する](performing-control-operations-on-a-socket.md)します。

WSK アプリケーションが、SIO WSK サブシステムでサポートされていない拡張機能インターフェイスのソケットを登録しようとしたかどうかは\_WSK\_登録\_拡張子ソケットの IOCTL 操作の状態が返されます\_されません\_サポートされています。

たとえば、次のコード例のように、拡張機能インターフェイスが定義されているとします。

```C++
const NPIID EXAMPLE_EXTIF_NPIID = {...};

typedef struct _EXAMPLE_EXTIF_PROVIDER_DISPATCH {
  .
  . // Function pointers for the functions that are
  . // defined by the extension interface.
  .
} EXAMPLE_EXTIF_PROVIDER_DISPATCH, *PEXAMPLE_EXTIF_PROVIDER_DISPATCH;

typedef struct _EXAMPLE_EXTIF_CLIENT_DISPATCH {
  .
  . // Function pointers for the callback functions
  . // that are defined by the extension interface.
  .
} EXAMPLE_EXTIF_CLIENT_DISPATCH, *PEXAMPLE_EXTIF_CLIENT_DISPATCH;
```

接続指向のソケットの場合は、この拡張機能インターフェイス WSK アプリケーションを登録する方法を次に示します。

```C++
// Client dispatch structure for the extension interface
const EXAMPLE_EXTIF_CLIENT_DISPATCH ExtIfClientDispatch = {
  .
  . // The WSK application's callback functions
  . // for the extension interface
  .
};

// Context structure type for the example extension interface
typedef struct _EXAMPLE_EXTIF_CLIENT_CONTEXT
{
  const EXAMPLE_EXTIF_PROVIDER_DISPATCH *ExtIfProviderDispatch;
  PVOID ExtIfProviderContext;
    .
    .  // Other application-specific members
    .
} EXAMPLE_EXTIF_CLIENT_CONTEXT, *PEXAMPLE_EXTIF_CLIENT_CONTEXT;

// Function to register the example extension interface
NTSTATUS
  RegisterExampleExtIf(
    PWSK_SOCKET Socket,
    PEXAMPLE_EXTIF_CLIENT_CONTEXT ExtIfClientContext
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  WSK_EXTENSION_CONTROL_IN ExtensionControlIn;
  WSK_EXTENSION_CONTROL_OUT ExtensionControlOut;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Fill in the WSK_EXTENSION_CONTROL_IN structure
  ExtensionControlIn.NpiId = &EXAMPLE_EXTIF_NPIID;
  ExtensionControlIn.ClientContext = ExtIfClientContext;
  ExtensionControlIn.ClientDispatch = &ExtIfClientDispatch;

  // Initiate the IOCTL operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskIoctl,
      SIO_WSK_REGISTER_EXTENSION,
      0,
      sizeof(WSK_EXTENSION_CONTROL_IN),
      &ExtensionControlIn,
      sizeof(WSK_EXTENSION_CONTROL_OUT),
      &ExtensionControlOut,
      NULL,
      NULL  // No IRP used for this IOCTL operation
      );

  // Check result
  if (Status == STATUS_SUCCESS)
  {
    // Save provider dispatch table and provider context
    ExtIfClientContext->ExtIfProviderDispatch =
      (const EXAMPLE_EXTIF_PROVIDER_DISPATCH *)
        ExtensionControlOut.ProviderDispatch;
    ExtIfClientContext->ExtIfProviderContext =
      ExtensionControlOut.ProviderContext;
  }

  // Return the status of the call to WskControlSocket()
  return Status;
}
```

ソケットのソケットによってごとに拡張機能インターフェイス WSK アプリケーションを登録します。

 

 





