---
title: ストライピング
description: ストライピング
ms.assetid: 29ab650c-0c3b-4693-a277-4d9ba63b7b66
keywords:
- ストライピング WDK オーディオ
- HD オーディオ、ストライピング
- 高解像度オーディオ (HD オーディオ)、ストライピング
- HD オーディオ、帯域幅
- 高解像度オーディオ (HD オーディオ)、帯域幅
- バスの帯域幅の WDK オーディオ
- 帯域幅の WDK オーディオ
- 帯域幅の割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa50f62832134b566fccdbb521fe5ae20d0d6f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354251"
---
# <a name="striping"></a>ストライピング


HD オーディオ アーキテクチャと呼ばれる手法をサポートしている*ストライピング*ストリームを表示するバスの帯域幅の量を削減することができますを使用します。 HD オーディオ ハードウェアのインターフェイスは、1 つ以上の SDO 行を提供する場合、ストライピングは、位置レンダリングの DMA エンジンは、または SDO 行の間でデータ ストリーム内のビットを分散することによってデータを転送できる速度を向上できます。 SDO0 経由 (最上位ビット) の最初のビット、2 番目のビットが SDO1、具合を介して送信されます。 たとえば、SDO の 2 行効果的にストライピングを 2 倍に転送速度 SDO の 2 行の間のストリームを分割することで。 ストライピングを使用して、レンダリングの転送が SDO の 2 つの行をストリームの DMA エンジンは、ストライピングを使用していない場合は消費するだけの半分のバス帯域幅を消費します。

関数のドライバーにより、を通じてストライピング、 [ **AllocateRenderDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンの*ストライプ*パラメーターを呼び出します。

ストライピングの詳細については、次を参照してください。、 *Intel 高度な定義オーディオ仕様*で、 [Intel HD オーディオ](https://go.microsoft.com/fwlink/p/?linkid=42508)web サイト。

 

 




