---
title: 線形のメモリ領域セグメント
description: 線形のメモリ領域セグメント
ms.assetid: c937eb39-b9ec-454e-98c5-7f5274328226
keywords:
- メモリセグメント WDK 表示、線形メモリスペースセグメント
- 線形メモリスペースセグメント WDK ディスプレイ
- メモリスペースセグメントの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b2434a41cb91a47ea46d17612e9bd4e7fe9c21f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840391"
---
# <a name="linear-memory-space-segments"></a>線形のメモリ領域セグメント


## <span id="ddk_linear_memory_space_segments_gg"></span><span id="DDK_LINEAR_MEMORY_SPACE_SEGMENTS_GG"></span>


線形メモリ空間セグメントは、ハードウェアが使用する従来の種類のセグメントです。 線形メモリ空間セグメントは、次のモデルに準拠しています。

-   グラフィックスアダプターにあるビデオメモリを仮想化します。

-   は GPU によって直接アクセスされます (つまり、ページマッピングを介してリダイレクトされることはありません)。

-   は、1次元のアドレス空間で直線的に管理されます。

ドライバーは、 [**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体の**Flags**メンバーを0に設定して、線形メモリスペースセグメントを指定します。 ただし、ドライバーは次のビットフィールドフラグを設定して、追加のセグメントのサポートを示すことができます。

-   CPU がアクセス可能であることを示すために**表示される**cpu。

-   セグメントが銀行に分割されていることを示すには、" **usebanking** " を指定します。

次の図は、線形メモリスペースセグメントを視覚的に表したものです。

![線形メモリスペースセグメントを示す図](images/memspac.png)

 

 





