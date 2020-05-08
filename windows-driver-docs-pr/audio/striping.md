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
ms.openlocfilehash: 71a555d4d503c169621692d2f2b3bf9717472e0b
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925515"
---
# <a name="striping"></a>ストライピング


HD オーディオアーキテクチャは*ストライピング*と呼ばれる手法をサポートしています。これにより、レンダーストリームで消費されるバス帯域幅の量を減らすことができます。 HD オーディオハードウェアインターフェイスに複数の SDO 線がある場合、ストライピングによって、データストリーム内のビットを SDO 行に分散させることで、レンダー DMA エンジンがデータを転送できる速度を上げることができます。 最初のビット (最上位ビット) は SDO0 を経由し、2番目のビットは SDO1 に移動します。 たとえば、2つの SDO 線を使用すると、ストライピングでは、2つの SDO 行の間にストリームを分割することで、転送速度を効率的に倍増させることができます。 ストライピングを使用して2つの SDO 行にレンダーストリームを転送する DMA エンジンでは、ストライピングを使用しなかった場合に消費されるバス帯域幅の半分しか消費されません。

関数ドライバーは、 [**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンの*ストライプ*呼び出しパラメーターを使用してストライピングを有効にします。

ストライピングの詳細については、intel [HD audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトの「 *Intel High Definition audio Specification* 」を参照してください。

 

 




