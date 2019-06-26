---
title: バンクへのメモリ領域セグメントの分割
description: バンクへのメモリ領域セグメントの分割
ms.assetid: 7fdbe511-ae92-44c2-9651-51b3ead11425
keywords:
- メモリのセグメントの WDK 表示、銀行
- バンク メモリ WDK の表示
- WDK の銀行を表示します。
- 線形のメモリ領域のセグメントの WDK の表示
- メモリのセグメントの WDK 表示、線形のメモリ領域のセグメント
- WDK の表示メモリ領域の線形セグメントに分割
- メモリ空間のセグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3267bd33f26eeda38ea3fded96ffb29ef4a97fcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365740"
---
# <a name="dividing-a-memory-space-segment-into-banks"></a>バンクへのメモリ領域セグメントの分割


## <span id="ddk_dividing_a_memory_space_segment_into_banks_gg"></span><span id="DDK_DIVIDING_A_MEMORY_SPACE_SEGMENT_INTO_BANKS_GG"></span>


ディスプレイのミニポート ドライバーはビデオ メモリ マネージャー内でのビデオのリソースの割り当ての最適な配置にきめ細かなヒントを提供することができます、[セグメントの線形のメモリ領域](linear-memory-space-segments.md)バンク メモリ (セグメントに分割して銀行)。 ドライバーは、銀行に線形のメモリ領域のセグメントを分割する場合、ドライバーを設定する必要があります、 **UseBanking**でフラグをビット フィールド、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)セグメントの構造体。 ドライバーはバンク メモリについてのヒントを返します、 **HintedBank**のメンバー [ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)割り当ての構造とビデオ メモリマネージャーは、ドライバーの[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数。 詳細については、次を参照してください。[割り当てを作成するときにセグメントを指定する](specifying-segments-when-creating-allocations.md)します。

割り当ては、セグメント内で完全に含まれる必要があります、中に、割り当ては、銀行、セグメント内の境界を越えることができます。

銀行を使用している場合、ドライバーには銀行のセグメントの全体のアドレス空間する必要がありますについて説明します。 最初の銀行が常に、セグメント内のオフセット 0 から開始し、最後の銀行が常に、セグメントの末尾で終了します。 銀行では、連続してあり、それらの間の空き領域がありません。

 

 





