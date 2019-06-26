---
title: 線形のアパーチャ領域セグメント
description: 線形のアパーチャ領域セグメント
ms.assetid: bf818841-eb73-442e-8745-a59d9c3a527c
keywords:
- メモリのセグメントの WDK 表示、線形 aperture 領域セグメント
- 線形 aperture 領域セグメント WDK の表示
- aperture 空間セグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629c9746aa1b4c8e5ecce5e3ce17dc7305ec84d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372916"
---
# <a name="linear-aperture-space-segments"></a>線形のアパーチャ領域セグメント


## <span id="ddk_linear_aperture_space_segments_gg"></span><span id="DDK_LINEAR_APERTURE_SPACE_SEGMENTS_GG"></span>


線形 aperture 領域セグメントは、線形のメモリ領域セグメントに似ていますただし、aperture 領域セグメントは、アドレス空間のみであり、ビットを保持することはできません。 ビットを保持するためには、システム メモリのページを割り当てる必要がある、およびそれらのページを参照するアドレス空間範囲をリダイレクトする必要があります。 ディスプレイのミニポート ドライバーを実装する必要があります、 [ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) DXGK 関数\_操作\_マップ\_APERTURE\_セグメントと DXGK\_操作\_UNMAP\_APERTURE\_リダイレクトを処理するために操作の種類をセグメント化し、」の説明に従って、この関数を公開する必要があります[ **表示のミニポート ドライバーの DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)します。 *DxgkDdiBuildPagingBuffer*関数は、リダイレクトする範囲と割り当てられた物理システム メモリ ページを参照する MDL を受け取ります。

通常、ディスプレイのミニポート ドライバーは、ビデオ メモリ マネージャーに既知でない、ページの表をプログラミングでアドレス空間範囲のリダイレクトを実現します。

ドライバーを設定する必要があります、 **Aperture**でフラグをビット フィールド、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)線形 aperture 領域セグメントを指定する構造体。 ドライバーでは、追加のセグメントのサポートを示すため、次のビット フィールド フラグも設定できます。

-   **CpuVisible**セグメントが CPU アクセス可能であることを示します。

-   **コヒーレント**をセグメントにセグメントがリダイレクトされるページの cpu 使用率とキャッシュの一貫性が管理していることを示します。

次の図は、線形 aperture 領域セグメントの視覚的表現を示します。

![線形 aperture 領域セグメントを示す図](images/aptrspac.png)

 

 





