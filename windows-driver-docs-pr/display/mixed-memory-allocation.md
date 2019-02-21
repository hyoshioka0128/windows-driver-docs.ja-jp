---
title: 混合メモリの割り当て
description: 混合メモリの割り当て
ms.assetid: 171efa48-bd1e-4545-a5c2-0b3ad4383448
keywords:
- WDK DirectDraw の混在のメモリ割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9740f8f9877d7d01e79e2b93a67e6c62247d9341
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535817"
---
# <a name="mixed-memory-allocation"></a>混合メモリの割り当て


## <span id="ddk_mixed_memory_allocation_gg"></span><span id="DDK_MIXED_MEMORY_ALLOCATION_GG"></span>


線形と四角形のメモリ ヒープを混合およびハードウェアがサポートされている場合、どのような形式は、一致することができます。 たとえば、フロント バッファーが固定ピッチの場合、DirectDraw 対応ドライバーは、右側に四角形のヒープを割り当てることができます。

主な領域の下に十分なメモリが残っている場合に、次の図に示すように、この領域は、バック バッファーのために使用する線形ヒープを作成できます。

![図に示すの混在のメモリ割り当て](images/ddfig6.png)

上記の図は、線形の主な領域 (ヒープ 1) の下のメモリと、四角形が、プライマリの画面 (ヒープ 2) の右側に DirectDraw によって解放されるメモリのです。

次の擬似コードに示す方法、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造が線形および四角形のメモリの組み合わせを設定します。

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] =
{
  { VIDMEM_ISRECTANGULAR, 0x00000000, 0x00000000,
            { 0 }, { 0 } },
  { VIDMEM_ISLINEAR, 0x00000000, 0x00000000,
            { 0 }, { 0 } },
};
```

表示メモリの 2 つの領域は、このインスタンスに割り当てることできます。 プライマリのサーフェスの概念の右側に領域は必ずしも四角形と、VIDMEM で示される\_ISRECTANGULAR フラグ。 概念的には、プライマリ画面下の領域は線形的で、できるし、VIDMEM で示される\_ISLINEAR フラグ。

次の疑似コードは、さまざまな線形および四角形のメモリ ヒープを設定する方法を示しています。

```cpp
/*
 * video memory pool information
 */

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList       = vidMem;

/* how many heaps are there   
     ddHALInfo.vmiData.dwNumHeaps       = 2;

/* The linear piece:  */


/*
 * remainder of screen memory
 */

    VideoHeapBase = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceSize
                    + dwCacheSize;
    VideoHeapEnd = VideoHeapBase + dwDDOffScreenSize - 1;
    vidMem[0].fpStart = VideoHeapBase;
    vidMem[0].fpEnd = VideoHeapEnd;

/* The rectangular piece:  */

/* set up the pointer to the next available video memory */
    ddHALInfo.vmiData.pvmList     = vidMem[1];

/*
 *  Compute the Pitch here ...
 */

    vidMem[1].fpStart  = ddHALInfo.vmiData.fpPrimary + 
                        dwPrimarySurfaceWidth;
    vidMem[1].dwWidth  = dwPitch - dwPrimarySurfaceWidth;
    vidMem[1].dwHeight = dwPrimarySurfaceHeight;
    vidMem[1].ddsCaps.dwCaps = 0;  // surface has no use restrictions
```

線形のメモリ ヒープを設定する開始点と、プライマリのサーフェイスの下のスクラッチ領域の終了点を特定することによって示される、 **fpStart**と**fpEnd** 、線形のメンバー [ **グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造 (<strong>vidMem\[</strong>0<strong>\]</strong>)。 四角形の部分がで示される、開始点を使用して設定、 **fpStart**四角形のグラフィックスアクセラレータ構造体のメンバー (<strong>vidMem\[</strong>1 <strong>\]</strong>)、によって示される、幅、 **dwWidth**によって示されるメンバー、および高さを**dwHeight**のプライマリ画面のメンバー。 ピッチ (、 **dwPitch**メンバー) 四角形の部分をセットアップする前に計算する必要があります。 これは、点を除いて、ピッチが 1 つ目ではなくグラフィックスアクセラレータ構造体の 2 番目の要素をここでは前の四角形の例のように同じです。 新しい各ヒープには、新しいグラフィックスアクセラレータ構造が必要です。

場合によっては、フリップ レジスタは 256 KB の境界のみを処理できます。 これらのインスタンスで小さなヒープは、キャッシュの下端とバック バッファーを 256 KB の境界で開始できるように、バック バッファーの先頭のスペースを使用できます。 この例は表示されませんが、グラフィックスアクセラレータ構造体を別の要素を追加し、キャッシュを越えた開始点と終点 256 KB の境界の直前に設定して実装できます。 DDSCAPS でこのようなヒープのフラグを設定する必要があります\_バックバッファー ヒープ マネージャーが、バック バッファーを検索するとき、その it をスキップするようにします。 このバック バッファー ヒープ (、1 つ配置) は、DDSCAPS でもマークは\_OFFSCREENPLAIN オフスクリーン サーフェスではプレーンなその他のヒープ内で使用可能なその他のメモリがなくなるまで、このヒープを使用してスプライトとテクスチャを保持します。

 

 





