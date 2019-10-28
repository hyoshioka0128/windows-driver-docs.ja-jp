---
title: 新しい Scatter/Gather DMA のサポート
description: 新しい Scatter/Gather DMA のサポート
ms.assetid: ac7cd98b-1211-4538-a54b-7362fa1d81b0
keywords:
- スキャッター/ギャザー DMA WDK ネットワーク
- ミニポートドライバー WDK ネットワーク、スキャッター/ギャザー DMA
- NDIS ミニポートドライバー WDK、スキャッター/ギャザー DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b944a8c1ba3a72fbd77f69dbc7cb716762ff4676
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842770"
---
# <a name="new-scattergather-dma-support"></a>新しい Scatter/Gather DMA のサポート





以前のバージョンの NDIS とは異なり、NDIS 6.0 では、パケットが DMA 転送用にマップされる前に、ミニポートドライバーに送信パケットが渡されます。 パケットを取得した後、ミニポートドライバーは、パケットのスキャッター/ギャザーリストを提供するように NDIS に要求できます。

これには次のようなメリットがあります。

-   ミニポートドライバーは、マップされる前にパケットにアクセスできるので、ミニポートドライバーがパケットに対して行う変更は、関連付けられているスキャッター/ギャザーリストのデータに反映されます。

-   ミニポートドライバーを使用すると、事前に割り当てられたバッファーにコピーすることによって、小さなまたは高度に断片化されたパケットの送信を最適化できます。これにより、マッピングは不要になります。 これにより、不要な処理が不要になります。

-   NDIS は、1つの関数呼び出しで複数の[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造をミニポートドライバーに安全に渡すことができます。 これにより、ミニポートドライバーの呼び出しが減るため、システムのパフォーマンスが向上します。

-   ミニポートドライバーはスキャッター/ギャザーリスト用にメモリを事前に割り当てることができるため、NDIS は実行時にスキャッター/ギャザーリストにメモリを割り当てる必要はありません。

NDIS 6.0 スキャッター/gather DMA の詳細については、「 [ndis 6.0 スキャッター/GATHER dma](ndis-scatter-gather-dma.md)」を参照してください。

 

 





