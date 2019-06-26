---
title: 割り当て作成時のセグメントの指定
description: 割り当て作成時のセグメントの指定
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- メモリのセグメントの WDK 表示、割り当ての作成
- WDK の割り当てを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56c7362a14741ba4ca5a7dce396a2fddedf6d915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376062"
---
# <a name="specifying-segments-when-creating-allocations"></a>割り当て作成時のセグメントの指定


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


ディスプレイのミニポート ドライバーを指定し、ビデオ メモリ マネージャーの使用が推奨ビデオ メモリ マネージャーがドライバーを呼び出すときにそのメモリ セグメントに関する情報を返します[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数。 呼び出しで*DxgkDdiCreateAllocation*ドライバーがビデオ リソースの割り当てを作成します。 ドライバーがサポートされるセグメントとセグメント各自の好みの識別子を返します、 [ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)の割り当てを記述する構造体。

返されるセグメントの情報からは、ビデオ メモリ マネージャーは、指定された操作のページで、適切なメモリ セグメントを決定します。

 

 





