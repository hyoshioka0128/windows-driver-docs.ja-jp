---
title: クライアント オブジェクトの制御操作の実行
description: クライアント オブジェクトの制御操作の実行
ms.assetid: 080c4821-43ea-4b6d-a55a-99621db17fb7
keywords:
- Winsock カーネル WDK がネットワーク接続、管理操作
- WSK WDK ネットワーク、管理操作
- WDK Winsock Kernel の動作を制御します。
- クライアント オブジェクト WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba4605f478ba9a30cc8363e2a8b1a542c09dc17b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377052"
---
# <a name="performing-control-operations-on-a-client-object"></a>クライアント オブジェクトの制御操作の実行


クライアント オブジェクトで管理操作を実行できます後は、Winsock カーネル (WSK) アプリケーションが正常に WSK サブシステムにアタッチと、( [ **WSK\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)) によって返された、添付ファイルの中に WSK サブシステムです。 これらのコントロールの操作では、特定のソケットに固有ではありませんが、代わりに一般的な範囲があります。 各クライアント オブジェクトで実行できる管理操作の詳細については、次を参照してください。 [WSK クライアントの管理操作](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client-control-operations)します。

WSK アプリケーションを呼び出してコントロールのクライアント操作を実行します、 [ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)関数。 **WskControlClient**関数で指し示されます、 **WskControlClient**のメンバー、 [ **WSK\_プロバイダー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)添付ファイルの中に、WSK サブシステムによって返された構造体。

次のコード例は、WSK アプリケーションの使用方法を示しています、 [ **WSK\_トランスポート\_一覧\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-transport-list-query)クライアント管理の操作の一覧を取得するには新しいソケットを作成するときに指定できる利用可能なネットワーク トランスポート。

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

 

 





