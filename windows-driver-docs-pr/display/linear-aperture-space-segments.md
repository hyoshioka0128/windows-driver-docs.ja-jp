---
title: 線形のアパーチャ領域セグメント
description: 線形のアパーチャ領域セグメント
ms.assetid: bf818841-eb73-442e-8745-a59d9c3a527c
keywords:
- メモリセグメント WDK 表示、線形アパーチャスペースセグメント
- 線形アパーチャ-スペースセグメントの WDK ディスプレイ
- アパーチャスペースセグメントの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7909593e5afe1423d2a0ff90784b0f544349f2a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840329"
---
# <a name="linear-aperture-space-segments"></a>線形のアパーチャ領域セグメント


## <span id="ddk_linear_aperture_space_segments_gg"></span><span id="DDK_LINEAR_APERTURE_SPACE_SEGMENTS_GG"></span>


線形のアパーチャ空間セグメントは、線形メモリスペースセグメントに似ています。ただし、アパーチャスペースセグメントはアドレス空間であるため、ビットを保持することはできません。 ビットを保持するには、システムメモリページを割り当てる必要があります。また、これらのページを参照するには、アドレス空間の範囲をリダイレクトする必要があります。 ディスプレイミニポートドライバーは、DXGK\_操作のための[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を実装する必要があります\_マップ\_アパーチャ\_セグメントと DXGK\_操作\_\_のアパーチャ\_セグメントをマップ解除リダイレクトを処理する操作の種類。「 [**Driverentry in The Display ミニポートドライバー**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)」で説明されているように、この関数を公開する必要があります。 *DxgkDdiBuildPagingBuffer*関数は、リダイレクトされる範囲と、割り当てられた物理システムメモリページを参照する MDL を受け取ります。

通常、ディスプレイミニポートドライバーは、ページテーブルをプログラミングすることによって、アドレス空間の範囲をリダイレクトします。これは、ビデオメモリマネージャーでは不明です。

ドライバーは、 [**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体の**Flags**メンバーで、**アパーチャ**ビットフィールドフラグを設定して、線形のアパーチャスペースセグメントを指定する必要があります。 ドライバーでは、次のビットフィールドフラグを設定して、追加のセグメントのサポートを示すこともできます。

-   CPU がアクセス可能であることを示すために**表示される**cpu。

-   **CacheCoherent**は、セグメントが、セグメントがリダイレクトされるページの CPU とキャッシュの一貫性を維持していることを示します。

次の図は、線形のアパーチャスペースセグメントの視覚的表現を示しています。

![線形のアパーチャスペースセグメントを示す図](images/aptrspac.png)

 

 





