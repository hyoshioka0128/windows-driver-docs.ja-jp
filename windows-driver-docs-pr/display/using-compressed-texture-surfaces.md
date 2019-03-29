---
title: 圧縮テクスチャ サーフェスの使用
description: 圧縮テクスチャ サーフェスの使用
ms.assetid: efa7efff-a1ad-49f3-b6e8-f08b520e77ae
keywords:
- 圧縮描画では、WDK DirectDraw をテクスチャ圧縮テクスチャ サーフェスについて
- 圧縮されたテクスチャ サーフェスに関する、DirectDraw 圧縮テクスチャ WDK Windows 2000 の表示します。
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、圧縮されたテクスチャ サーフェスについて
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
- rasterizers WDK DirectDraw を参照します。
- rasterizers WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88457f90904660b129113cfa9cba967d83db152c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350369"
---
# <a name="using-compressed-texture-surfaces"></a>圧縮テクスチャ サーフェスの使用


## <span id="ddk_using_compressed_texture_surfaces_gg"></span><span id="DDK_USING_COMPRESSED_TEXTURE_SURFACES_GG"></span>


DirectDraw のみ同じ DXT 型の 2 つの画面間の blt を行う場合、ドライバーを呼び出して、DDCAPS2\_COPYFOURCC フラグに設定されて、 **dwCaps2**のメンバー、 [ **DDCORECAPS**](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造体。 このフラグが設定されていない場合、DirectDraw HEL は、blt を実行します。 これは、機能は、メモリを表示するサーフェスを (システム メモリ) をバックアップからのテクスチャをダウンロードするためのメカニズムは、このため、画面に表示のコピーの blt をバックアップするために重要です。 したがって、DXT テクスチャ サーフェスを効果的に公開する必要があります、DDCAPS2 をサポートするために、ドライバー\_COPYFOURCC フラグ。

DDCAPS2\_COPYFOURCC フラグがいくつかの問題。 ドライバーは、少なくともこれらの属性を持つ FOURCC 形式の間での blt を実行できる必要があります。

-   ソースと変換先の形式は、同じ FOURCC 形式です。

-   ソースと宛先表面が異なります。

-   サーフェス全体を行うと、ソースと変換先の四角形 (つまり、ストレッチはありません、subrectangles はありません)。

-   表示メモリは両方のサーフェスです。

-   ドライバーは、表示メモリでは、すべての FOURCC 形式のこれらの転送を実行できる必要があります。

**注**   DirectShow、DDCAPS2 を使用して\_COPYFOURCC フラグ; 一部のビデオ機能を高速化をこのフラグの要件はすべて FOURCC 形式がコピーされることを意味します。

 

Blt 操作の DXT 形式に圧縮する場合は、DirectDraw HEL は常に、blt を行います。 これは、DirectDraw が、ドライバーを blt を実行することを要求することを意味します。

-   宛先表面には、DXT 形式があります。

-   ソースと宛先表面の形式は、同じではありません。

DirectDraw DDCAPS のセマンティクス\_CANBLTSYSMEM 機能ビットがメモリを表示するシステム メモリからすべての転送、ディスプレイ ドライバーが呼び出されることを意味します。 その結果、ドライバーから呼び出すことがこのような転送 DXT サーフェス DXT 非サーフェスにします。 ドライバーは、DDHAL を返す唯一の要件がここでは\_ドライバー\_NOTHANDLED、圧縮解除を実行できない場合。 これにより、DDERR を伝達する DirectDraw\_アプリケーションにサポートされていないエラー コード。 ドライバーでは、メモリを表示するシステム メモリから転送の圧縮解除を実装することができますが、これは DirectX 6.0 およびそれ以降のバージョンでは必要ありません。

DirectDraw 表示のメモリ割り当てルーチンは、ピクセル形式に関する考慮事項を処理しないでください。 [**HeapVidMemAllocAligned**](https://msdn.microsoft.com/library/windows/hardware/ff567267)、たとえばは、入力パラメーターとしてバイト数が必要です。 同様に、DDHAL\_PLEASEALLOC\_BLOCKSIZE (を参照してください、 **fpVidMem**のメンバー、 [ **DD\_画面\_GLOBAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551726)構造) ことを示す、 **dwBlockSizeX**と**dwBlockSizeY** 、DD のメンバー\_画面\_グローバル構造体はバイト数と、行の数それぞれします。 その結果、ドライバーは、DirectDraw アロケーターを介して表示メモリを割り当て、これらのメカニズムのいずれかを使用している場合、ドライバーは、メモリ使用量、(バイト単位) を単独で DXT サーフェスを計算することである必要があります。 次の例は、この計算を実行する 1 つの方法を示しています。

```cpp
DWORD dx, dy;
DWORD blksize, surfsize;
LPVOID pmem;

/*
 * Determine how much memory to allocate for the FOURCC format.
 */
switch ((int)pDDPF->dwFourCC)
{
  case MAKEFOURCC('D','X','T','1'):
    blksize = 8; // The size of a DXT1 4x4 pixel block. 
    break;
  case MAKEFOURCC('D','X','T','2'):    // premultiplied alpha
  case MAKEFOURCC('D','X','T','3'):    // non-premultiplied alpha
    blksize = 16; //The size of a DXT2,3 4x4 pixel block 
    break;
  case MAKEFOURCC('D','X','T','4'):    // premultiplied alpha
  case MAKEFOURCC('D','X','T','5'):    // non-premultiplied alpha
    blksize = 16; //The size of a DXT4,5 4x4 pixel block.
  break;

  default:
    DDASSERT(0);
}

/*
 * Calculate the number of blocks in the x and y dimensions.
 */
dx = (nWidth  + 3) >> 2;
dy = (nHeight + 3) >> 2;
surfsize = dx * dy * blksize;
```

アプリケーションを呼び出すと、 **IDirect3DVertexBuffer7::Lock**または**IDirectDrawSurface7::GetSurfaceDesc** (それぞれ、Direct3D、DirectDraw SDK のドキュメント セットで説明) メソッド圧縮の画面で、ドライバーが、DDSD を設定する必要があります\_LINEARSIZE フラグ、 **dwFlags**のメンバー、 [ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)構造体。 さらに、ドライバーが圧縮された画面のデータが含まれてに割り当てられたバイト数を設定する必要があります、 **dwLinearSize**同じ構造体のメンバー。 (、 **DwLinearSize**共用体のメンバーが存在する、 **lPitch**メンバー、これらのメンバーが相互に排他的では、DDSD\_LINEARSIZE と DDSD\_ピッチ フラグ)。

ハードウェアまたはドライバーは、変換し、(通常、順序変更ハードウェア効率的なレイアウトに) を選択した任意の形式で圧縮したテクスチャを格納します。 ただし、ハードウェアまたはドライバーできる必要があります DirectDraw で必要なつまり、アプリケーションが呼び出すたびにされるたびに、元の DXT コード形式に圧縮テクスチャを変換する、 **IDirect3DVertexBuffer7::Lock**メソッド.

### <a name="span-idwindows2000notespanspan-idwindows2000notespanwindows-2000-note"></a><span id="windows_2000_note"></span><span id="WINDOWS_2000_NOTE"></span>Windows 2000 に注意してください。

Windows 2000 ではいくつかのメモリ割り当てのためにマップされているフィールドは、システム メモリ DXT サーフェスがありました。 マッピングは次のとおりです。

```cpp
wWidth = lPitch = dx * blksize;
wHeight         = dy;
dwRGBBitCount   = 8;
```

ドライバーが検出した場合、システム メモリ DXT 画面などで[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)、作成する前にフェールバックするフィールドをマップする必要がありますの使用。 戻すマッピングです。

```cpp
realWidth        = (wWidth  << 2) / blksize;
realHeight       =  wHeight << 2;
realLinearSize   = dwLinearSize * wHeight;
realRGBBitCount  = 0
```

### <a name="span-idreferencerasterizernotesspanspan-idreferencerasterizernotesspanreference-rasterizer-notes"></a><span id="reference_rasterizer_notes"></span><span id="REFERENCE_RASTERIZER_NOTES"></span>リファレンス ラスタライザーのノート

次の 3 つの項目は、リファレンス ラスタライザー (RefRast) コードを実装するときに従ってください。

1.  セクション「 *3 ビット アルファ Linear (DXT4 および DXT5 形式)* DirectDraw SDK ドキュメントは DXT4 および DXT5 形式のアルファ値を強化するための正しい順序を示しています。

2.  リファレンス ラスタライザーのコードでは、色の比較ロジックを保護する次のロジックが必要です。
    ```cpp
    if ((color_0 > color_1) OR !DXT1) {
    /*  color comparison logic */
    }
    ```

3.  参照 rasterizers のハードウェアの実装がより少し異なる方法で、元の値を推定する計算式の丸め処理を実行できるため、テストをカラーとアルファ値がから取得したで若干のバリエーションを許可する必要があります、圧縮解除のロジックです。

 

 





