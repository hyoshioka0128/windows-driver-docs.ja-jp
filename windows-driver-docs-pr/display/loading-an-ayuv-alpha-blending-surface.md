---
title: AYUV アルファ ブレンド サーフェスの読み込み
description: AYUV アルファ ブレンド サーフェスの読み込み
ms.assetid: 93b60622-47af-485c-a1db-9a05783ff698
keywords:
- alpha-blend データ読み込み (WDK DirectX VA)
- 画像のブレンド WDK DirectX VA、アルファブレンドデータ読み込み
- AYUV アルファブレンドサーフェス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4665b576250c3110d00cd0e59a8fac6a40562c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840390"
---
# <a name="loading-an-ayuv-alpha-blending-surface"></a>AYUV アルファ ブレンド サーフェスの読み込み


## <span id="ddk_loading_an_ayuv_alpha_blending_surface_gg"></span><span id="DDK_LOADING_AN_AYUV_ALPHA_BLENDING_SURFACE_GG"></span>


AYUV のアルファブレンドサーフェイスは、 [**DXVA\_AYUVsample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2)構造体のそれぞれ32ビットのサンプルの配列として定義されています。 このサーフェイスは、デコードされたビデオ画像とグラフィックをブレンドするためのソースとして使用できます。

AYUV のアルファブレンドサーフェイスの幅と高さは、関連付けられている [[バッファーの説明] の一覧](buffer-description-list.md)で指定します。

### <a name="span-idloading_a_16-entry_yuv_palettespanspan-idloading_a_16-entry_yuv_palettespanspan-idloading_a_16-entry_yuv_palettespanloading-a-16-entry-yuv-palette"></a><span id="Loading_a_16-Entry_YUV_Palette"></span><span id="loading_a_16-entry_yuv_palette"></span><span id="LOADING_A_16-ENTRY_YUV_PALETTE"></span>16エントリの YUV パレットを読み込んでいます

16エントリの YUV パレットは、16個の[**DXVA\_AYUVsample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2)構造体の配列として定義されます。 このパレットは、IA44 または AI44 のアルファブレンドサーフェイスと共に使用されます。 パレット配列は、AYUV のアルファブレンディングサンプルバッファー (バッファーの種類 8) でアクセラレータに送信されます。 この場合、各サンプルの DXVA\_AYUVsample2 構造体の**bSampleAlpha8**メンバーは意味がなく、0である必要があります。

YUV パレットを使用すると、デコードされたビデオ画像とグラフィックをブレンドするためのソースを作成できます。 このパレットは、次のいずれかと共にグラフィックソースを作成するために使用できます。

-   IA44/ *AI44 のアルファ*ブレンドサーフェイス。

-   [アルファブレンド] 画面、強調表示バッファー、および DCCMD データを選択します。

### <a name="span-idloading_an_ayuv_surfacespanspan-idloading_an_ayuv_surfacespanspan-idloading_an_ayuv_surfacespanloading-an-ayuv-surface"></a><span id="Loading_an_AYUV_Surface"></span><span id="loading_an_ayuv_surface"></span><span id="LOADING_AN_AYUV_SURFACE"></span>AYUV サーフェスを読み込んでいます

画像グラフィック全体は、16入力パレットだけを読み込むのではなく、単に AYUV イメージとして直接読み込んでグラフィックコンテンツを指定できます。 この場合、 [**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)構造体で指定されているように、ayuv グラフィックは、ayuv アルファブレンディングサンプルバッファー (バッファーの種類 8) でアクセラレータに送信されます。

### <a name="span-idloading_an_ia44_ai44_alpha-blending_surfacespanspan-idloading_an_ia44_ai44_alpha-blending_surfacespanspan-idloading_an_ia44_ai44_alpha-blending_surfacespanloading-an-ia44ai44-alpha-blending-surface"></a><span id="Loading_an_IA44_AI44_Alpha-Blending_Surface"></span><span id="loading_an_ia44_ai44_alpha-blending_surface"></span><span id="LOADING_AN_IA44_AI44_ALPHA-BLENDING_SURFACE"></span>IA44/AI44 のアルファブレンド画面の読み込み

インデックスアルファ 4-4 (IA44) のアルファブレンドサーフェイスは、8ビットのサンプルの配列として定義されており、それぞれがバイトとして構成されています。 このバイトは*DXVA\_IA44sample*と呼ばれ、 *DXVA*で定義されています。 このバイトの最上位4ビットには、 *SampleIndex4*と呼ばれるインデックスが含まれています。このバイトの最下位4ビットには、 *SampleAlpha4*と呼ばれるアルファ値が含まれています。

Alpha-index 4-4 (AI44) のアルファブレンドサーフェイスは、8ビットのサンプルの配列として定義されており、それぞれがバイトとして構成されています。 このバイトは*DXVA\_AI44sample*と呼ばれ、 *DXVA*で定義されています。 このバイトの最上位4ビットには、 *SampleAlpha4*と呼ばれるアルファ値が含まれています。このバイトの最下位4ビットには、 *SampleIndex4*と呼ばれるインデックスが含まれています。

*DXVA\_IA44sample*と*DXVA\_AI44sample*の両方の*SampleIndex4*フィールドには、サンプルの16入力パレットのインデックスが含まれています。

*DXVA\_IA44sample*と*DXVA\_AI44sample*の両方の*SampleAlpha4*フィールドには、サンプルの不透明度を指定する次の値が含まれています。

-   ゼロは、サンプルが透明であることを示します ( *SampleIndex4*のパレットエントリが結果のブレンド画像に影響を与えないようにするため)。 *SampleAlpha4*の値が0の場合、blend では、画像の値を変更せずに使用します。

-   値15は、サンプルが不透明であることを示します。これにより、 *SampleIndex4*のパレットエントリによって、結果のブレンド画像が完全に決定されます。

-   0以外の値は、指定された blend が次の式によって検出されることを示します。

((*SampleAlpha4*+ 1) x グラフィック\_value + (15-*SampleAlpha4*) x picture\_value + 8) &gt;&gt; 4

IA44 のアルファブレンドサーフェイスの幅と高さは、関連付けられている [[バッファーの説明] の一覧](buffer-description-list.md)で指定します。

 

 





