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
ms.openlocfilehash: 37c33669d826048428025bfc781d1040ad37c3d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582151"
---
# <a name="performing-control-operations-on-a-client-object"></a>クライアント オブジェクトの制御操作の実行


クライアント オブジェクトで管理操作を実行できます後は、Winsock カーネル (WSK) アプリケーションが正常に WSK サブシステムにアタッチと、( [ **WSK\_クライアント**](https://msdn.microsoft.com/library/windows/hardware/ff571155)) によって返された、添付ファイルの中に WSK サブシステムです。 これらのコントロールの操作では、特定のソケットに固有ではありませんが、代わりに一般的な範囲があります。 各クライアント オブジェクトで実行できる管理操作の詳細については、[WSK クライアントの管理操作](https://msdn.microsoft.com/library/windows/hardware/ff571157)を参照してください。

WSK アプリケーションを呼び出してコントロールのクライアント操作を実行します、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数。 **WskControlClient**関数で指し示されます、 **WskControlClient**のメンバー、 [ **WSK\_プロバイダー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571175)添付ファイルの中に、WSK サブシステムによって返された構造体。

次のコード例は、WSK アプリケーションの使用方法を示しています、 [ **WSK\_トランスポート\_一覧\_クエリ**](https://msdn.microsoft.com/library/windows/hardware/ff571195)クライアント管理の操作の一覧を取得するには新しいソケットを作成するときに指定できる利用可能なネットワーク トランスポート。

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

 

 





