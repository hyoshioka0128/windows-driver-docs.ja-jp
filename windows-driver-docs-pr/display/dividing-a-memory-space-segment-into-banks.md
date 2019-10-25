---
title: バンクへのメモリ領域セグメントの分割
description: バンクへのメモリ領域セグメントの分割
ms.assetid: 7fdbe511-ae92-44c2-9651-51b3ead11425
keywords:
- メモリセグメント WDK 表示、銀行
- 銀行のメモリの WDK ディスプレイ
- 銀行の WDK ディスプレイ
- 線形メモリスペースセグメント WDK ディスプレイ
- メモリセグメント WDK 表示、線形メモリスペースセグメント
- 線形メモリスペースセグメントの分割 WDK 表示
- メモリスペースセグメントの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb776c3191f1704e056622aa75a781835823eaf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838990"
---
# <a name="dividing-a-memory-space-segment-into-banks"></a>バンクへのメモリ領域セグメントの分割


## <span id="ddk_dividing_a_memory_space_segment_into_banks_gg"></span><span id="DDK_DIVIDING_A_MEMORY_SPACE_SEGMENT_INTO_BANKS_GG"></span>


ディスプレイミニポートドライバーは、セグメントをバンク的メモリ (銀行) に分割することによって、[線形メモリ空間セグメント](linear-memory-space-segments.md)内のビデオリソースの割り当てに最適な配置について、詳細なヒントをビデオメモリマネージャーに提供できます。 ドライバーが線形メモリ空間セグメントを銀行に分割する場合、ドライバーはセグメントの[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体の**Flags**メンバーで**usebanking**ビットフィールドフラグを設定する必要があります。 このドライバーは、ビデオメモリマネージャーがドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を呼び出したときに割り当てを行うために、 **HintedBank**メンバーの[ **\_DXGK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)のメンバーであるバンクメモリに関するヒントを返します。 詳細については、「[割り当てを作成するときのセグメントの指定](specifying-segments-when-creating-allocations.md)」を参照してください。

割り当てはセグメント内に完全に含まれている必要がありますが、割り当てはセグメント内の銀行の境界を越えることができます。

銀行が使用されている場合、ドライバーは、バンクを含むセグメントのアドレス空間全体をカバーする必要があります。 最初のバンクは、常にセグメント内のオフセット0から開始され、最後のバンクは常にセグメントの最後で終了します。 銀行は連続していて、それらの間に空き領域がありません。

 

 





