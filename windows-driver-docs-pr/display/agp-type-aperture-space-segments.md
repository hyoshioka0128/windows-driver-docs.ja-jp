---
title: AGP タイプのアパーチャ領域セグメント
description: AGP タイプのアパーチャ領域セグメント
ms.assetid: a531f79e-541a-4454-8337-19a99aa046ae
keywords:
- メモリのセグメントの WDK 表示、AGP 型 aperture 領域セグメント
- AGP 型 aperture 領域セグメント WDK の表示
- aperture 空間セグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8b24145b1658b293f2725e72e09d89549f7c8ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381886"
---
# <a name="agp-type-aperture-space-segments"></a>AGP タイプのアパーチャ領域セグメント


## <span id="ddk_agp_type_aperture_space_segments_gg"></span><span id="DDK_AGP_TYPE_APERTURE_SPACE_SEGMENTS_GG"></span>


AGP 型の開口部領域セグメントは、線形 aperture 領域セグメントに似ていますただし、表示のミニポート ドライバーでは DXGK を公開しません\_操作\_マップ\_APERTURE\_セグメントと DXGK\_操作\_UNMAP\_APERTURE\_のセグメントの操作の種類、 [ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) AGP 型 aperture 領域のセグメントを使用してコールバック関数。 ビデオ メモリ マネージャーは GART ドライバーを使用して、マップおよびシステム ページをマップ解除する代わりに、(つまり、ビデオ メモリ マネージャーは実行されません、ディスプレイのミニポート ドライバー)。

ドライバーを設定する必要があります、 **Agp**でフラグをビット フィールド、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体AGP 型 aperture 領域セグメントを指定します。

 

 





