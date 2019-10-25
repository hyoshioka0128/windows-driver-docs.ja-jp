---
title: DMA バッファーの修正プログラムの適用
description: DMA バッファーの修正プログラムの適用
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA バッファー WDK 表示、修正プログラム
- DMA バッファーの修正プログラムの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f71ff78483e7221df2230c3849b9cf36cd52253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829865"
---
# <a name="patching-a-dma-buffer"></a>DMA バッファーの修正プログラムの適用


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


DMA バッファーのすべてのメモリリソースが格納されていることがビデオメモリマネージャーに通知された後、GPU スケジューラはディスプレイミニポートドライバーの[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)関数を呼び出して、物理アドレスを使用してリソースにパッチを適用します (つまり、物理アドレスを割り当てます。リソースへのアドレス)。

 

 





