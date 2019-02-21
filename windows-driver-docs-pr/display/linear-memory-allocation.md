---
title: 線形のメモリの割り当て
description: 線形のメモリの割り当て
ms.assetid: f39c6752-c771-43d4-b89e-77f3d542d1fd
keywords:
- 線形のメモリ割り当て WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6632a5c20124b7db1f08b0333bdd77bf20c85a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532887"
---
# <a name="linear-memory-allocation"></a>線形のメモリの割り当て


## <span id="ddk_linear_memory_allocation_gg"></span><span id="DDK_LINEAR_MEMORY_ALLOCATION_GG"></span>


表示メモリと見なされます*線形*(ように、次の図に示す) のアカウントの配置の要件を声の高さは、画面の幅に合わせて変更できます、されるたびが考慮されます。 たとえば、ブリット機能が 8 バイトの前進をのみヒットし、31 ピクセルのスプライトを使用した場合の表示の各行を 8 バイト境界には、次の行に合わせていずれかで調整する必要があります。

ピッチはアカウントの配置の要件を考慮して、画面の幅 (バイト単位)、ピクセルの深度を掛けることによって決定されます。 表示が 640 8 ビット ピクセルの場合は、ピッチは 640 です。 ピクセルが 16 ビットである場合 (2 バイト)、640 X 480 の画面があるし、声の高さが 1280 (640 \* 2)。 同様に、2560 の声の高さのある 640 ワイド、32 ビット (4 バイト) ピクセルの画面 (640 \* 4) 線形表示メモリでします。

次の図は、1 つのプライマリ画面および 1 つのスクラッチ領域を持つ線形のメモリ ヒープの割り当てを示しています。

![線形のメモリ ヒープの割り当てを示す図](images/ddfig4.png)

プライマリのサーフェスの先頭へのポインターが**fpPrimary**のメンバー、 [ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)構造体。 指定したプライマリ サーフェスとキャッシュは、このスクラッチ領域の先頭へのポインターを提供するさまざまな Windows のサイズ、 **fpStart**のメンバー、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造体。 によって示される、終点、 **fpEnd**のメンバー、**グラフィックスアクセラレータ**構造体から 1 を引いたの残りのメモリのサイズを加算して計算されます。

[**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造体は、ヒープ表示のメモリを管理する情報を保持します。 このサンプルの配列で 1 つだけの要素には**グラフィックスアクセラレータ**構造体の 1 つだけのヒープがあるためです。 VIDMEM\_ISLINEAR、フラグ、 **dwFlags**のメンバー、**グラフィックスアクセラレータ**構造体、これを線形のメモリとして表します。

次の擬似コードに示す方法、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)構造が線形のメモリを設定します。

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISLINEAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};/*
```

次の疑似コードは、ヒープを設定する方法の線形のメモリを示します。

```cpp
/*
 * video memory pool information
 */

/* Calculate the number of video memory heaps */
    ddHALInfo.vmiData.dwNumHeaps = sizeof ( vidMem ) / sizeof ( vidMem [ 0 ] );

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList     = vidMem;

/*
 * remainder of screen memory
 */

    VideoHeapBase = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceSize + dwCacheSize;
    VideoHeapEnd = VideoHeapBase + dwDDOffScreenSize - 1;

    vidMem[ 0 ].fpStart = VideoHeapBase;
    vidMem[ 0 ].fpEnd = VideoHeapEnd;
```

最初の使用可能なスクラッチ領域の先頭は、プライマリの画面のサイズを Windows ブラシ、ペン、および VDD キャッシュのサイズ、GDI のプライマリ画面の先頭を加算して計算されます。 最初の要素の開始点を設定するため、結果、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)スクラッチ領域の先頭に構造体。

スクラッチ領域の末尾は、スクラッチ領域のサイズをスクラッチ領域の先頭を追加し、包括的にするには、1 を減算して検出されます。 結果の最初の (および、この場合は、のみ) エンド ポイント要素を設定するため、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)スクラッチ領域の末尾に構造体。 複数のヒープがある場合、開始位置がこの終点がこのヒープと [次へ] のヒープの末尾に設定します。

 

 





