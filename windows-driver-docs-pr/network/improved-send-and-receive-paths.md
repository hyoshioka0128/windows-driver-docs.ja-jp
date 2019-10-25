---
title: 送信および受信パスの改善
description: 送信および受信パスの改善
ms.assetid: 7edecb49-576f-4058-92e8-39f14268a130
keywords:
- NDIS WDK、送受信 (データを)
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9f2f76835eede23309aa5da68b362719853714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827356"
---
# <a name="improved-send-and-receive-paths"></a>送信および受信パスの改善





NDIS 6.0 の送信パスと受信パスは、パフォーマンスを向上させるために次のように改善されています。

-   すべての NDIS 6.0 以降のドライバー送信および受信関数は、1つの関数呼び出しを使用して、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体とそれに関連付けられた[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造のリンクリストを転送できます。 このようなマルチパケットの送信操作と受信操作をサポートすることで、ドライバーが行う必要がある関数呼び出しの数を大幅に減らすことができます。

-   送信または受信機能を呼び出すときに、ディスパッチ\_レベルで実行されているドライバーは、NDIS への IRQL を示すことができます。 その後、NDIS がスタック内の他のドライバーの呼び出しを行う場合、これらのドライバーが IRQL をテストしたり、\_レベルをディスパッチするように設定したりする必要はありません。 これにより、重要なコードセクションでの IRQL のテストと設定に関連するオーバーヘッドが軽減されます。

-   ドライバースタックにパケットが渡されると、ドライバーは、ヘッダー情報に対応するように、NET\_バッファーのデータオフセットを調整するように NDIS に要求できます。 ドライバーは、パケットを送信するときに、ドライバーのヘッダー情報を格納するために、使用されているデータ領域を拡張できます。 受信パケットを示す場合、ドライバーは、ヘッダー情報へのアクセスが完了した後で、使用されているデータ領域を減らすことができます。 この機能により、使用されているデータ領域を NET\_のバッファー構造で動的に調整できます。メモリの割り当てや解放、データのコピーは行われません。これにより、ネットワークデータの処理に必要なオーバーヘッドが軽減されます。

NDIS 6.0 で送受信されるデータ処理の詳細については、「 [NET\_のバッファーアーキテクチャ](net-buffer-architecture.md)」を参照してください。

 

 





