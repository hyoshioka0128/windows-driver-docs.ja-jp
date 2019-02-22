---
title: AYUV アルファ ブレンドの読み込み画面
description: AYUV アルファ ブレンドの読み込み画面
ms.assetid: 93b60622-47af-485c-a1db-9a05783ff698
keywords:
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
- AYUV アルファ ブレンド画面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27309f40e7e9c1a9f178714e0ef257862ca5bf4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556465"
---
# <a name="loading-an-ayuv-alpha-blending-surface"></a>AYUV アルファ ブレンドの読み込み画面


## <span id="ddk_loading_an_ayuv_alpha_blending_surface_gg"></span><span id="DDK_LOADING_AN_AYUV_ALPHA_BLENDING_SURFACE_GG"></span>


AYUV アルファ ブレンドの画面は、32 のサンプルの配列をビットのそれぞれに定義されて、 [ **DXVA\_AYUVsample2** ](https://msdn.microsoft.com/library/windows/hardware/ff563116)構造体。 この画面は、デコードされたビデオ画像のグラフィックをブレンドするためのソースとして使用できます。

幅と AYUV アルファ ブレンド画面の高さが指定されて、関連付けられた[バッファー記述リスト](buffer-description-list.md)します。

### <a name="span-idloadinga16-entryyuvpalettespanspan-idloadinga16-entryyuvpalettespanspan-idloadinga16-entryyuvpalettespanloading-a-16-entry-yuv-palette"></a><span id="Loading_a_16-Entry_YUV_Palette"></span><span id="loading_a_16-entry_yuv_palette"></span><span id="LOADING_A_16-ENTRY_YUV_PALETTE"></span>16 エントリ YUV パレットの読み込み

16 エントリ YUV パレットが 16 の配列として定義されている[ **DXVA\_AYUVsample2** ](https://msdn.microsoft.com/library/windows/hardware/ff563116)構造体。 このパレットは、IA44 または AI44 アルファ ブレンド画面と共に使用されます。 パレットの配列は、AYUV アルファ ブレンド サンプル バッファーにアクセラレータに送信されます (バッファーの種類 8)。 ここで、 **bSampleAlpha8**メンバーは、DXVA の\_AYUVsample2 構造の各サンプルに意味がなく、ゼロにする必要があります。

YUV パレットは、デコードされたビデオ画像のグラフィックスの描画のソースの作成に使用できます。 このパレットは、いずれかと共に画像のソースを作成するために使用できます。

-   IA44/AI44 アルファ ブレンドの画面には、*または*

-   DPXD アルファ ブレンドの画面、強調表示バッファー、および DCCMD データ

### <a name="span-idloadinganayuvsurfacespanspan-idloadinganayuvsurfacespanspan-idloadinganayuvsurfacespanloading-an-ayuv-surface"></a><span id="Loading_an_AYUV_Surface"></span><span id="loading_an_ayuv_surface"></span><span id="LOADING_AN_AYUV_SURFACE"></span>AYUV、画面の読み込み

パレットを 16 エントリだけを読み込むのではなく、イメージ全体のグラフィックは、グラフィックのコンテンツを指定する AYUV イメージとして直接単純に読み込まれます。 この場合は、AYUV グラフィックは AYUV アルファ ブレンド サンプル バッファーにアクセラレータに送信 (バッファーの種類 8) で指定されている、 [ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)構造体。

### <a name="span-idloadingania44ai44alpha-blendingsurfacespanspan-idloadingania44ai44alpha-blendingsurfacespanspan-idloadingania44ai44alpha-blendingsurfacespanloading-an-ia44ai44-alpha-blending-surface"></a><span id="Loading_an_IA44_AI44_Alpha-Blending_Surface"></span><span id="loading_an_ia44_ai44_alpha-blending_surface"></span><span id="LOADING_AN_IA44_AI44_ALPHA-BLENDING_SURFACE"></span>IA44/AI44 アルファ ブレンドのサーフェイスの読み込み

インデックス-alpha 4-4 (IA44) アルファ ブレンドの画面が 8 ビットのサンプルのそれぞれの構造をバイトとしての配列として定義されます。 このバイトと呼びます*DXVA\_IA44sample*で定義されていると*dxva.h*します。 このバイトの 4 つの最上位ビットと呼ばれるインデックスが含まれて*SampleIndex4*、このバイトの 4 つの最下位ビットと呼ばれる、アルファ値を格納および*SampleAlpha4*します。

アルファ-インデックス 4-4 (AI44) アルファ ブレンドの画面が 8 ビットのサンプルのそれぞれの構造をバイトとしての配列として定義されます。 このバイトと呼びます*DXVA\_AI44sample*で定義されていると*dxva.h*します。 このバイトの 4 つの最上位ビットと呼ばれる、アルファ値を格納*SampleAlpha4*このバイトの 4 つの最下位ビットと呼ばれるインデックスを含めることが*SampleIndex4*します。

*SampleIndex4*両方のフィールド*DXVA\_IA44sample*と*DXVA\_AI44sample*の 16 エントリ パレットに、インデックスが含まれています、サンプルです。

*SampleAlpha4*両方のフィールド*DXVA\_IA44sample*と*DXVA\_AI44sample*不透明度を指定するには、次の値が含まれていますサンプル。

-   0 は、サンプルが透明であることを示します (ようにパレット エントリ*SampleIndex4*組み合わせた結果の画像に影響を与えません)。 0 個の値の*SampleAlpha4*、指定された blend は、画像の変更を加えることがなく値を使用します。

-   15 文字の値は、サンプルが不透明であることを示します (ようにパレット エントリ*SampleIndex4*組み合わせた結果の画像を完全に決定します)。

-   0 以外の値は、次の式で指定された blend が見つかったことを示します。

((*SampleAlpha4*+1) グラフィック X\_値 + (15 -*SampleAlpha4*) 画像 X\_値 + 8) &gt; &gt; 4

幅と IA44 アルファ ブレンド画面の高さが指定されて、関連付けられた[バッファー記述リスト](buffer-description-list.md)します。

 

 





