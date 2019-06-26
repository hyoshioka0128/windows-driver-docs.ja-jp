---
title: ネットワーク データ構造
description: ネットワーク データ構造
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c5534ae67d8e5ffb3358b0a75346b56b302817e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386221"
---
# <a name="network-data-structures"></a>ネットワーク データ構造





ネットワーク経由で送受信データのパケットのネットワーク データで構成されます。 NDIS は、記述し、このようなデータを整理するデータ構造体を提供します。 NDIS 6.0 以降のプライマリ ネットワーク データの構造は次のとおりです。

-   [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)
-   [**NET\_バッファーの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)
-   [**NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)

次の図は、これらの構造体間のリレーションシップを示しています。

![図に示す ndis 6.0 ネットワークのデータ構造体](images/netbufferstructures.png)

NDIS 6.0 以降では、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)はネットワーク データをパッケージ化するための基本的な構成要素です。 各ネット\_バッファーの構造体が、MDL チェーン。 データのアドレスは、データをバッファー MDLs マップ領域を NET\_バッファーの構造体を指定します。 このデータ マッピングのと同じですが、MDL チェーンその NDIS 5。*x*で以前のドライバーを使用して、 [ **NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造体。 NDIS は、MDL チェーンを操作する関数を提供します。

複数の NET\_バッファーの構造体は、NET にアタッチできる\_バッファー\_リスト構造体。 NET\_バッファーの構造体が NULL で終わるシングル リンク リストとして構成されています。 NET の発生元のドライバーだけ\_バッファー\_リスト構造体、または NDIS、挿入および削除の NET に直接リンク リストを変更する必要があります\_バッファーの構造体。

[**NET\_バッファー リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体には、すべてを記述する情報が含まれて、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)リストにアタッチされている構造体。 NET に、ドライバーがこのような情報を格納、ドライバーは、コンテキスト情報の追加の領域を必要とする場合\_バッファー\_一覧\_CONTEXT 構造体。 NDIS を割り当て、およびネットワーク内のデータ アクセス機能を提供する\_バッファー\_一覧\_CONTEXT 構造体。

複数の NET\_バッファー\_NET のリストを形成するリストの構造体を接続できる\_バッファー\_リストの構造体。 NET\_バッファー\_リストの構造体が NULL で終わるシングル リンク リストとして構成されています。 ドライバーは、挿入および削除の NET に直接リンク リストを変更できます\_バッファー\_リストの構造体。

## <a name="related-topics"></a>関連トピック


[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)

[NET\_バッファーの構造体](net-buffer-structure.md)

[**NET\_バッファーの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[NET\_バッファー\_リスト構造](net-buffer-list-structure.md)

[**NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)

[NET\_バッファー\_一覧\_CONTEXT 構造体](net-buffer-list-context-structure.md)

 

 






