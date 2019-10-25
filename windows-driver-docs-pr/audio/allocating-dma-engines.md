---
title: DMA エンジンの割り当て
description: DMA エンジンの割り当て
ms.assetid: 45b772ce-e6ae-4102-bad4-734f8f079817
keywords:
- HD オーディオ、DMA エンジン
- High Definition Audio (HD audio)、DMA エンジン
- DMA エンジンの割り当て
- DMA エンジン割り当て WDK オーディオ
- DMA エンジン WDK オーディオをレンダリングする
- DMA エンジン WDK オーディオをキャプチャする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0a63f634d2d204c043d22b38f1f776a4d846b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831585"
---
# <a name="allocating-dma-engines"></a>DMA エンジンの割り当て


HD オーディオコントローラーには、固定された数の DMA エンジンが含まれています。 各エンジンは、1つのレンダーストリームまたはキャプチャストリームに対して、スキャッター/ギャザー転送を実行できます。

次の3種類の DMA エンジンを使用できます。

-   レンダーストリームのみを処理できる DMA エンジンをレンダリングします。

-   キャプチャストリームのみを処理できる DMA エンジンをキャプチャします。

-   双方向 DMA エンジン。レンダーストリームまたはキャプチャストリームを処理するように構成できます。

レンダーストリームの DMA エンジンを割り当てるときに、使用可能な場合は、 [**Allocatecapturedmaengine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)ルーチンによってレンダー DMA エンジンが割り当てられます。 レンダー DMA エンジンの提供が終了した場合、ルーチンは、使用可能な場合は双方向 DMA エンジンを割り当てます。

同様に、キャプチャストリームに DMA エンジンを割り当てる場合、 [**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンはキャプチャ dma エンジンが使用可能な場合はそれを割り当てます。 キャプチャ DMA エンジンの提供が終了した場合、ルーチンは、使用可能な場合は双方向 DMA エンジンを割り当てます。

Allocate*Xxx*DmaEngine ルーチンは、HD audio DDI の両方のバージョンで使用できます。

 

 




