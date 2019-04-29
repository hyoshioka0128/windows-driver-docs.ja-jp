---
title: DMA バッファーの準備
description: DMA バッファーの準備
ms.assetid: 9231badb-7b42-46d1-95f6-34c0ec7ab3cb
keywords:
- DMA バッファー WDK の表示の準備
- GPU の枯渇 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 051cec0f0fd66b39e8c3306f08934528c54574fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383924"
---
# <a name="preparing-dma-buffers"></a>DMA バッファーの準備


## <span id="ddk_preparing_dma_buffers_gg"></span><span id="DDK_PREPARING_DMA_BUFFERS_GG"></span>


ディスプレイのミニポート ドライバーでは、適切なタイミングで DMA バッファーを準備する必要があります。 GPU は、DMA バッファーを処理するときに通常ディスプレイのミニポート ドライバーと呼ばれる、時に、GPU に送信する次の DMA バッファーを準備します。 GPU の枯渇を防ぐためには、ディスプレイのミニポート ドライバーを準備して、GPU は、現在の DMA バッファーの処理よりも、後続の DMA バッファーを送信する時間が短縮する必要があります。

 

 





