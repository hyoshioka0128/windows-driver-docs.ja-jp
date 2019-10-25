---
title: クライアント オブジェクトの制御操作の実行
description: クライアント オブジェクトの制御操作の実行
ms.assetid: 080c4821-43ea-4b6d-a55a-99621db17fb7
keywords:
- Winsock カーネル WDK ネットワーク、制御操作
- WSK WDK ネットワーク、制御操作
- コントロール操作 WDK Winsock カーネル
- クライアントオブジェクト WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680527a1ef9a0054e84fc73312f5a62ea1bb3a62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843689"
---
# <a name="performing-control-operations-on-a-client-object"></a>クライアント オブジェクトの制御操作の実行


Winsock カーネル (WSK) アプリケーションが WSK サブシステムに正常にアタッチされると、添付中に WSK サブシステムから返されたクライアントオブジェクト ( [**wsk\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)) に対して制御操作を実行できます。 これらの制御操作は、特定のソケットに固有のものではなく、より一般的なスコープを持ちます。 クライアントオブジェクトで実行できる各制御操作の詳細については、「 [Wsk クライアント制御操作](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client-control-operations)」を参照してください。

WSK アプリケーションは、 [**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出すことによって、クライアントの制御操作を実行します。 **Wskcontrolclient**関数は、 [**WSK\_PROVIDER\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)の渡し、wsk サブシステムから返されたディスパッチ構造体の**wskcontrolclient**メンバーによって示されます。

次のコード例では、WSK アプリケーションが[**wsk\_TRANSPORT\_\_list**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-transport-list-query)を使用してクライアントコントロール操作のクエリを実行し、新しいソケットの作成時に指定できる利用可能なネットワークトランスポートの一覧を取得する方法を示します。

```C++
// Function to retrieve a list of available network transports
NTSTATUS
  GetTransportList(
    PWSK_PROVIDER_NPI WskProviderNpi,
    PWSK_TRANSPORT TransportList,
    ULONG MaxTransports,
    PULONG TransportsRetrieved
    )
{
  SIZE_T BytesRetrieved;
  NTSTATUS Status;

  // Perform client control operation
  Status =
    WskProviderNpi->Dispatch->
        WskControlClient(
          WskProviderNpi->Client,
          WSK_TRANSPORT_LIST_QUERY,
          0,
          NULL,
          MaxTransports * sizeof(WSK_TRANSPORT),
          TransportList,
          &BytesRetrieved,
          NULL  // No IRP for this control operation
          );

  // Convert bytes retrieved to transports retrieved
  TransportsRetrieved = BytesRetrieved / sizeof(WSK_TRANSPORT);

  // Return status of client control operation
  return Status;
}
```

 

 





