---
title: 四角形のメモリの割り当て
description: 四角形のメモリの割り当て
ms.assetid: 27e60130-3a6e-410a-86a7-19acad5ecb53
keywords:
- 四角形のメモリ割り当て WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 771eb07b14039e986bb71780aab07d3a5426010b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351481"
---
# <a name="rectangular-memory-allocation"></a>四角形のメモリの割り当て


## <span id="ddk_rectangular_memory_allocation_gg"></span><span id="DDK_RECTANGULAR_MEMORY_ALLOCATION_GG"></span>


表示メモリと見なされます*四角形*声の高さを指定されたヒープ内のすべてのサーフェイスに特定のサイズに固定するたびにします。

四角形の表示のメモリ レイアウトは、有限の幅と高さで 2 次元です。 この幅は常に画面の幅と同じです。 表示メモリは、別のディスプレイ解像度と設計に関する考慮事項を考慮する必要があります、ためです実際の水平方向の幅は、モニターに現在表示されてよりもはるかに大きいリージョンをまたがる場合があります。 メモリのヒープ割り当てのように、ピッチの値は次のスキャン ラインの表示メモリの同じ列を達成するためにメモリの表示の列に追加するバイトの数に基づきます。

たとえば、場合でも、四角形の表示メモリが 8 ビットのピクセルの間で 1280 バイトである場合に、画面が、640 ピクセルを表示する可能性があります、1280 (640 ではありません) は、声の高さにします。 16 ビットのピクセルを使用してメモリの 1280 ピクセルの水平方向 stretch でピッチは 2560 です。 8 ビット (ピクセル単位) には、32 ビット ピクセルの声の高さが 4 倍ピッチは 5120 で表示が 1280 32 ビット ピクセルの場合。

通常、四角形のメモリは小さなフラグメントがアプリケーションで大きなサーフェイスを格納した後に残る可能性がありますのでに線形メモリよりもアプリケーションによって効率も下がります使用されます。 アプリケーションは、残りの領域で使用可能なバイト数が、新しい画面を必要とより大きい場合でも、残りの領域に他の面を格納することができない可能性があります。 アプリケーションは、先着順では、この領域にアクセスできるし、残りのフラグメントにのみに適合する小規模のサーフェスを格納できます。

四角形のヒープは、使用可能なメモリは、連続した領域にすることはできません L 型ため、そのサイズは、X の Y 座標で測定されます。 四角形のヒープが高さと幅プライマリ画面を保持するのに十分ではない場合、バック バッファーをすることはできません。 プライマリのサーフェスのピッチでプライマリ画面の表示幅と等しくない場合は、四角形の表示の概念の右側にメモリ ブロックを残された (ヒープは、次の図 1)。 このブロックは、ディスプレイの幅から引いたピッチの幅と同じです。 右側に残っているメモリ場合にも発生線形のカードで、既存のディスプレイ ドライバーが固定ピッチを前提としています。 主な領域の下 (ただし、この例ではなく)、または四角形の直線上のメモリで残っても可能性があります。

次の図は、四角形のメモリの割り当てを示しています。

![四角形のメモリの割り当てを示す図](images/ddfig5.png)

上記の図では、開始点 (によって示される、 **fpStart**のメンバー、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造) の四角形のヒープを加算して計算されます、プライマリの画面の開始アドレスへのプライマリ画面の幅。 幅と高さは、四角形のヒープのサイズにも計算されます。 以下の Windows のキャッシュ メモリが残っている場合があります、ヒープを作成できます。

次の擬似コードに示す方法、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造が四角形のメモリを設定します。

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISRECTANGULAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};
```

四角形のメモリのコードと対応する線形の唯一の違いは、VIDMEM\_ISRECTANGULAR フラグは、四角形のメモリであることを示します

次の疑似コードは、ヒープを設定する方法の四角形のメモリを示します。

```cpp
/*
 * video memory pool information
 */

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList      = vidMem;

/* this is set to zero because there may only be one heap depending on the pitch 
    ddHALInfo.vmiData.dwNumHeaps      = 0; 


/*
 *  Compute the Pitch here ...
 */


    vidMem[0].fpStart  = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceWidth;
    vidMem[0].dwWidth  = dwPitch - dwPrimarySurfaceWidth;
    vidMem[0].dwHeight = dwPrimarySurfaceHeight;
    vidMem[0].ddsCaps.dwCaps = 0;      // surface has no use restrictions
```

開始位置、メモリ ヒープは、プライマリの画面の開始アドレスと、プライマリの画面の幅に設定されます。 幅は、プライマリの画面の幅を引いた、声の高さによって決まります。 高さは、プライマリの画面の高さに設定されます。 サーフェイスの機能が課せられてサーフェスの使用に関する制限がないことを示すゼロに設定されます (そのため、サーフェスをスプライトまたは画面の他の任意の型に使用できます)。

 

 





