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
ms.openlocfilehash: 5da5e760db98f5c43cd2bc0f8cea1ace51cdc59a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354239"
---
# <a name="linear-aperture-space-segments"></a>線形のアパーチャ領域セグメント


## <span id="ddk_linear_aperture_space_segments_gg"></span><span id="DDK_LINEAR_APERTURE_SPACE_SEGMENTS_GG"></span>


線形 aperture 領域セグメントは、線形のメモリ領域セグメントに似ていますただし、aperture 領域セグメントは、アドレス空間のみであり、ビットを保持することはできません。 ビットを保持するためには、システム メモリのページを割り当てる必要がある、およびそれらのページを参照するアドレス空間範囲をリダイレクトする必要があります。 ディスプレイのミニポート ドライバーを実装する必要があります、 [ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587) DXGK 関数\_操作\_マップ\_APERTURE\_セグメントと DXGK\_操作\_UNMAP\_APERTURE\_リダイレクトを処理するために操作の種類をセグメント化し、」の説明に従って、この関数を公開する必要があります[ **表示のミニポート ドライバーの DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556157)します。 *DxgkDdiBuildPagingBuffer*関数は、リダイレクトする範囲と割り当てられた物理システム メモリ ページを参照する MDL を受け取ります。

通常、ディスプレイのミニポート ドライバーは、ビデオ メモリ マネージャーに既知でない、ページの表をプログラミングでアドレス空間範囲のリダイレクトを実現します。

ドライバーを設定する必要があります、 **Aperture**でフラグをビット フィールド、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)線形 aperture 領域セグメントを指定する構造体。 ドライバーでは、追加のセグメントのサポートを示すため、次のビット フィールド フラグも設定できます。

-   **CpuVisible**セグメントが CPU アクセス可能であることを示します。

-   **コヒーレント**をセグメントにセグメントがリダイレクトされるページの cpu 使用率とキャッシュの一貫性が管理していることを示します。

次の図は、線形 aperture 領域セグメントの視覚的表現を示します。

![線形 aperture 領域セグメントを示す図](images/aptrspac.png)

 

 





