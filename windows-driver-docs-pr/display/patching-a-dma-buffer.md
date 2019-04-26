---
title: DMA バッファーの修正プログラムの適用
description: DMA バッファーの修正プログラムの適用
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA バッファー WDK の表示、修正プログラムの適用
- WDK の表示の DMA バッファー修正プログラムの適用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4a5196bf04475a8f03795e0b7379f8f6d333e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352397"
---
# <a name="patching-a-dma-buffer"></a>DMA バッファーの修正プログラムの適用


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


マネージャーの通知後ビデオ メモリ GPU スケジューラにディスプレイ ミニポート ドライバーの呼び出し、DMA バッファーのすべてのメモリ リソースが配置されている[ **DxgkDdiPatch** ](https://msdn.microsoft.com/library/windows/hardware/ff559737)リソースにパッチを適用する関数物理アドレス (リソースには、物理アドレスを割り当て、)。

 

 





