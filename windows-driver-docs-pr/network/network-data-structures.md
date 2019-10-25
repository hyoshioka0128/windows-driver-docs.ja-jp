---
title: ネットワーク データ構造
description: ネットワーク データ構造
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
- パケット WDK ネットワーク, データ構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28de665bbeacbfd2e568eb758847197b7c1f69fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827244"
---
# <a name="network-data-structures"></a>ネットワーク データ構造





ネットワークデータは、ネットワーク経由で送受信されるデータのパケットで構成されます。 NDIS には、そのようなデータを記述および整理するためのデータ構造が用意されています。 NDIS 6.0 以降のプライマリネットワークデータ構造は次のとおりです。

-   [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)
-   [**NET\_バッファーの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)
-   [**NET\_BUFFER\_LIST\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

次の図は、これらの構造間の関係を示しています。

![ndis 6.0 ネットワークデータ構造を示す図](images/netbufferstructures.png)

NDIS 6.0 以降では、ネットワークデータをパッケージ化するための基本的な構成要素として、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)が使用されます。 各 NET\_バッファー構造体には、MDL チェーンがあります。 MDLs は、データバッファーのアドレスを、NET\_BUFFER 構造体で指定されたデータ領域にマップします。 このデータマッピングは、NDIS 5 と同じ MDL チェーンと同じです。*x*以前のドライバーは、 [**NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造で使用されます。 NDIS には、MDL チェーンを操作する関数が用意されています。

Net\_BUFFER\_LIST 構造体には、複数の NET\_バッファー構造体をアタッチできます。 NET\_バッファー構造は、NULL で終わる単一のシングルリンクリストとして構成されます。 Net\_BUFFER\_LIST 構造体または NDIS の生成元であるドライバーだけが、リンクリストを変更して、NET\_バッファー構造を挿入および削除する必要があります。

[**Net\_バッファーリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、リストにアタッチされているすべての[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を記述する情報が含まれています。 ドライバーがコンテキスト情報用に追加の領域を必要とする場合、ドライバーは、そのような情報を NET\_BUFFER\_LIST\_CONTEXT 構造体に格納できます。 NDIS には、NET\_BUFFER\_LIST\_CONTEXT 構造体のデータを割り当て、解放し、アクセスするための関数が用意されています。

複数の NET\_バッファー\_リスト構造をアタッチして、NET\_BUFFER\_リスト構造のリストを形成できます。 NET\_BUFFER\_LIST 構造体は、NULL で終わる単一のシングルリンクリストとして構成されます。 ドライバーは、リンクリストを直接変更して、NET\_BUFFER\_LIST 構造体を挿入および削除することができます。

## <a name="related-topics"></a>関連トピック


[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)

[NET\_のバッファー構造](net-buffer-structure.md)

[**NET\_バッファーの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[NET\_BUFFER\_LIST 構造体](net-buffer-list-structure.md)

[**NET\_BUFFER\_LIST\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

[NET\_BUFFER\_LIST\_CONTEXT 構造体](net-buffer-list-context-structure.md)

 

 






