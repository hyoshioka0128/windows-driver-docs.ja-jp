---
title: 割り当て作成時のセグメントの指定
description: 割り当て作成時のセグメントの指定
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- メモリセグメント WDK ディスプレイ、割り当ての作成
- 割り当て WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86fdda890a99b56d812a02a0c2431b1668debe7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829441"
---
# <a name="specifying-segments-when-creating-allocations"></a>割り当て作成時のセグメントの指定


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


ディスプレイミニポートドライバーは、ビデオメモリマネージャーがドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を呼び出したときに、ビデオメモリマネージャーによって使用されることが推奨されるメモリセグメントに関する情報を指定して返します。 *DxgkDdiCreateAllocation*の呼び出しでは、ドライバーはビデオリソースの割り当てを作成します。 ドライバーは、割り当てを記述する[**DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)の割り当て情報の構造体でサポートされているセグメントとセグメントの設定の識別子を返します。

ビデオメモリマネージャーは、返されたセグメント情報から、指定された操作のための適切なメモリセグメントを特定のページに配置します。

 

 





