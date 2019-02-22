---
title: セグメントの線形のメモリ領域
description: セグメントの線形のメモリ領域
ms.assetid: c937eb39-b9ec-454e-98c5-7f5274328226
keywords:
- メモリのセグメントの WDK 表示、線形のメモリ領域のセグメント
- 線形のメモリ領域のセグメントの WDK の表示
- メモリ空間のセグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd6f6f0d76197f83abd89257d97368dfa3bff75a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530632"
---
# <a name="linear-memory-space-segments"></a>セグメントの線形のメモリ領域


## <span id="ddk_linear_memory_space_segments_gg"></span><span id="DDK_LINEAR_MEMORY_SPACE_SEGMENTS_GG"></span>


メモリ領域の直線セグメントは、ハードウェアの使用方法を表示するセグメントの従来の型です。 メモリ領域の直線セグメントでは、次のモデルに準拠しています。

-   グラフィックス アダプター上にあるビデオ メモリを仮想化します。

-   GPU から直接アクセスは (つまり、ページ マッピングを通じてリダイレクトなし)。

-   1 次元のアドレス空間では直線的に管理されます。

ドライバーのセット、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)メモリ領域の直線セグメントを指定する 0 に構造体。 ただし、ドライバーは、次のビット フィールドを追加のセグメントのサポートを示すためにフラグを設定できます。

-   **CpuVisible**セグメントが CPU アクセス可能であることを示します。

-   **UseBanking**を銀行にセグメントが分割されているかを示します。

次の図は、メモリ領域の直線セグメントの視覚的表現を示します。

![メモリ領域の直線セグメントを示す図](images/memspac.png)

 

 





