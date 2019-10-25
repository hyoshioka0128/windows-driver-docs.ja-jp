---
title: ストライピング
description: ストライピング
ms.assetid: 29ab650c-0c3b-4693-a277-4d9ba63b7b66
keywords:
- WDK オーディオのストライピング
- HD オーディオ、ストライピング
- High Definition Audio (HD audio)、ストライピング
- HD オーディオ、帯域幅
- High Definition Audio (HD audio)、帯域幅
- バス帯域幅 WDK オーディオ
- 帯域幅 WDK オーディオ
- 帯域幅の割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a002afac326d572af80849061048870fa59a651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830105"
---
# <a name="striping"></a>ストライピング


HD オーディオアーキテクチャは*ストライピング*と呼ばれる手法をサポートしています。これにより、レンダーストリームで消費されるバス帯域幅の量を減らすことができます。 HD オーディオハードウェアインターフェイスに複数の SDO 線がある場合、ストライピングによって、データストリーム内のビットを SDO 行に分散させることで、レンダー DMA エンジンがデータを転送できる速度を上げることができます。 最初のビット (最上位ビット) は SDO0 を経由し、2番目のビットは SDO1 に移動します。 たとえば、2つの SDO 線を使用すると、ストライピングでは、2つの SDO 行の間にストリームを分割することで、転送速度を効率的に倍増させることができます。 ストライピングを使用して2つの SDO 行にレンダーストリームを転送する DMA エンジンでは、ストライピングを使用しなかった場合に消費されるバス帯域幅の半分しか消費されません。

関数ドライバーは、 [**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンの*ストライプ*呼び出しパラメーターを使用してストライピングを有効にします。

ストライピングの詳細については、intel [HD audio](https://go.microsoft.com/fwlink/p/?linkid=42508) web サイトの「 *Intel High Definition audio Specification* 」を参照してください。

 

 




