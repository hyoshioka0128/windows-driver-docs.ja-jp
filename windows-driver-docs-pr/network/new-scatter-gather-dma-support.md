---
title: 新しい Scatter/Gather DMA のサポート
description: 新しい Scatter/Gather DMA のサポート
ms.assetid: ac7cd98b-1211-4538-a54b-7362fa1d81b0
keywords:
- スキャッター/ギャザー ネットワーク DMA WDK
- ミニポート ドライバー WDK スキャッター/ギャザー DMA ネットワーク、
- NDIS ミニポート ドライバー WDK、スキャッター/ギャザー DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6965f102a6ec4834e5f03d6a8313d9452d3d729
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371218"
---
# <a name="new-scattergather-dma-support"></a>新しい Scatter/Gather DMA のサポート





NDIS の以前のバージョンとは異なり NDIS 6.0 では DMA の転送パケットがマップされる前に、送信パケットをミニポート ドライバーに渡します。 パケットが取得して、ミニポート ドライバーは、パケットのスキャッター/ギャザーの一覧を指定する NDIS を要求できます。

これには次のようなメリットがあります。

-   マップする前に、ミニポート ドライバーには、パケットへのアクセスがあるために、ミニポート ドライバーがパケットに変更が関連付けられているスキャッター/ギャザー リストのデータに反映されます。

-   ミニポート ドライバーでは、マッピングの必要がなくなります、事前に割り当てられるバッファーにコピーすることで、小規模または高度に断片化されたパケットの送信を最適化できます。 これにより、不要な処理がなくなります。

-   NDIS は複数に安全に渡すことができます[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)ミニポート ドライバーが 1 つの関数呼び出しに構造体。 これによってミニポート ドライバーに少ない呼び出しになり、システム パフォーマンスが向上します。

-   ミニポート ドライバーがスキャッター/ギャザーの一覧については、メモリ事前割り当てを行うことができますので、NDIS がスキャッター/ギャザー リストの実行時にメモリを割り当てることはありません。

NDIS 6.0 のスキャッター/ギャザー DMA の詳細については、次を参照してください。 [NDIS 6.0 のスキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)します。

 

 





