---
title: DMA エンジンの割り当て
description: DMA エンジンの割り当て
ms.assetid: 45b772ce-e6ae-4102-bad4-734f8f079817
keywords:
- HD オーディオ、DMA エンジン
- Hd オーディオ (HD オーディオ)、DMA エンジン
- 割り当ての DMA エンジン
- DMA エンジン割り当て WDK オーディオ
- DMA エンジン WDK オーディオをレンダリングします。
- DMA エンジン WDK オーディオをキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0040102cbb768bbb5a972f70e1c1272fb6cf4d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355767"
---
# <a name="allocating-dma-engines"></a>DMA エンジンの割り当て


HD オーディオ コント ローラーには、固定数 DMA エンジンにはが含まれています。 各エンジンでは、1 つのレンダーのスキャッター/ギャザーの転送を実行したり、ストリームをキャプチャすることができます。

次の 3 つの種類の DMA エンジンを使用できます。

-   レンダリング ストリームのみを処理できるは、DMA エンジンをレンダリングします。

-   キャプチャ ストリームのみを処理できるは、DMA エンジンをキャプチャします。

-   双方向の DMA エンジンには、いずれかのレンダリングを処理またはストリームをキャプチャするように構成できます。

レンダリングのストリームの DMA エンジンを割り当てるときに、 [ **AllocateCaptureDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)ルーチンが使用できる場合、レンダリングの DMA エンジンを割り当てます。 DMA エンジンをレンダリングする場合は、終了ルーチンが使用できる場合、双方向の DMA エンジンを割り当てます。

同様に、ときに、DMA を割り当てエンジン ストリームについては、キャプチャ、 [ **AllocateRenderDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンが使用できる場合、キャプチャの DMA エンジンを割り当てます。 DMA エンジンをキャプチャする場合は、終了ルーチンが使用できる場合、双方向の DMA エンジンを割り当てます。

割り当て*Xxx*DmaEngine ルーチンは、HD オーディオ DDI の両方のバージョンで使用できます。

 

 




