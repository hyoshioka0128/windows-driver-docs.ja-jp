---
title: 拡張インターフェイスの登録
description: 拡張インターフェイスの登録
ms.assetid: 33dc32da-9bc1-40b4-8737-ec132ec36708
keywords:
- Winsock カーネル WDK ネットワーク、拡張インターフェイス
- WSK WDK ネットワーク、拡張インターフェイス
- 拡張機能インターフェイス WDK Winsock カーネル
- Winsock カーネル拡張インターフェイスを登録しています
- SIO_WSK_REGISTER_EXTENSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 239551ec06e469d25ae0d3dcea43f1931ea35159
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842094"
---
# <a name="registering-an-extension-interface"></a>拡張インターフェイスの登録


Winsock カーネル (WSK) アプリケーションでソケットが正常に作成されると、WSK サブシステムでサポートされている1つ以上の[拡張インターフェイス](winsock-kernel-extension-interfaces.md)にそのソケットを登録できます。 Wsk サブシステムによってサポートされる拡張インターフェイスのセットは、wsk サブシステムによってアプリケーションに返される wsk [ **\_プロバイダー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)構造体の**バージョン**メンバーを調べることによって、wsk アプリケーションによって決定されます。添付中。

各拡張インターフェイスは、WSK NPI に依存しない NPI によって定義されます。 ただし、拡張インターフェイスの NPIs では、NPI 固有の特性がサポートされていないことに注意してください。

WSK アプリケーションは、 [**SIO\_WSK\_REGISTER\_extension**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-register-extension) socket IOCTL 操作をソケットに登録して、拡張インターフェイスを登録します。 ソケットの IOCTL 操作の実行の詳細については、「[ソケットでの制御操作の実行](performing-control-operations-on-a-socket.md)」を参照してください。

Wsk アプリケーションが WSK サブシステムでサポートされていない拡張インターフェイスのソケットを登録しようとした場合、SIO\_WSK\_レジスタ\_拡張ソケットの IOCTL 操作は、サポートされて\_いない状態\_ステータスを返します。

たとえば、次のコード例では、拡張インターフェイスがとして定義されているとします。

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

次に示すのは、WSK アプリケーションが接続指向ソケットのこの拡張インターフェイスに登録する方法を示しています。

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

WSK アプリケーションは、ソケットごとに拡張インターフェイスを登録します。

 

 





