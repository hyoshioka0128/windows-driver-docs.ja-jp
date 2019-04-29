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
ms.openlocfilehash: fc3c75b99ec958b9ae183d3ef54e6c33683f3ef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331728"
---
# <a name="allocating-dma-engines"></a>DMA エンジンの割り当て


HD オーディオ コント ローラーには、固定数 DMA エンジンにはが含まれています。 各エンジンでは、1 つのレンダーのスキャッター/ギャザーの転送を実行したり、ストリームをキャプチャすることができます。

次の 3 つの種類の DMA エンジンを使用できます。

-   レンダリング ストリームのみを処理できるは、DMA エンジンをレンダリングします。

-   キャプチャ ストリームのみを処理できるは、DMA エンジンをキャプチャします。

-   双方向の DMA エンジンには、いずれかのレンダリングを処理またはストリームをキャプチャするように構成できます。

レンダリングのストリームの DMA エンジンを割り当てるときに、 [ **AllocateCaptureDmaEngine** ](https://msdn.microsoft.com/library/windows/hardware/ff536177)ルーチンが使用できる場合、レンダリングの DMA エンジンを割り当てます。 DMA エンジンをレンダリングする場合は、終了ルーチンが使用できる場合、双方向の DMA エンジンを割り当てます。

同様に、ときに、DMA を割り当てエンジン ストリームについては、キャプチャ、 [ **AllocateRenderDmaEngine** ](https://msdn.microsoft.com/library/windows/hardware/ff536181)ルーチンが使用できる場合、キャプチャの DMA エンジンを割り当てます。 DMA エンジンをキャプチャする場合は、終了ルーチンが使用できる場合、双方向の DMA エンジンを割り当てます。

割り当て*Xxx*DmaEngine ルーチンは、HD オーディオ DDI の両方のバージョンで使用できます。

 

 




