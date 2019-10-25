---
title: AGP 型のアパーチャスペースセグメント
description: AGP 型のアパーチャスペースセグメント
ms.assetid: a531f79e-541a-4454-8337-19a99aa046ae
keywords:
- メモリセグメント WDK ディスプレイ、AGP タイプのアパーチャスペースセグメント
- AGP タイプのアパーチャ-スペースセグメントの WDK ディスプレイ
- アパーチャスペースセグメントの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb4d8bda3852129028a05bdfa53fb03b127aeb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839078"
---
# <a name="agp-type-aperture-space-segments"></a>AGP 型のアパーチャスペースセグメント


## <span id="ddk_agp_type_aperture_space_segments_gg"></span><span id="DDK_AGP_TYPE_APERTURE_SPACE_SEGMENTS_GG"></span>


AGP 型のアパーチャスペースセグメントは、線形のアパーチャスペースセグメントに似ています。ただし、ディスプレイミニポートドライバーでは、DXGK\_操作\_マップ\_アパーチャ\_セグメントおよび DXGK\_操作が公開されていません。\_、 [**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)コールバック関数は、AGP 型のアパーチャスペースセグメントを経由します。\_\_ 代わりに、ビデオメモリマネージャーは、GART ドライバーを使用してシステムページをマップおよびマップ解除します (つまり、ビデオメモリマネージャーにはディスプレイミニポートドライバーは含まれません)。

ドライバーは、 [**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体の**Flags**メンバーで**agp**ビットフィールドフラグを設定して、agp 型のアパーチャスペースセグメントを指定する必要があります。

 

 





