---
title: DMA バッファーの修正プログラムの適用
description: DMA バッファーの修正プログラムの適用
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA バッファー WDK の表示、修正プログラムの適用
- WDK の表示の DMA バッファー修正プログラムの適用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339587a7d528cea029b277c61a3a31b5f399b9db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377373"
---
# <a name="patching-a-dma-buffer"></a>DMA バッファーの修正プログラムの適用


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


マネージャーの通知後ビデオ メモリ GPU スケジューラにディスプレイ ミニポート ドライバーの呼び出し、DMA バッファーのすべてのメモリ リソースが配置されている[ **DxgkDdiPatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)リソースにパッチを適用する関数物理アドレス (リソースには、物理アドレスを割り当て、)。

 

 





