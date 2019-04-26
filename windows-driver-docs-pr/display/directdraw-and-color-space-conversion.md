---
title: DirectDraw と色空間変換
description: DirectDraw と色空間変換
ms.assetid: 2a5e59ea-2190-4701-ab7b-7a6503aec6e5
keywords:
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw、色空間の変換
- DirectDraw 中 WDK Windows 2000 の表示、色空間の変換
- WDK DirectDraw、色空間の変換中
- blt WDK DirectDraw、色空間の変換
- YUV は、WDK DirectDraw を書式設定します。
- Fourcc
- 色空間 WDK DirectDraw
- 色空間を変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69d786d137f5f7e0559539afa9e31c9ff581e77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358258"
---
# <a name="directdraw-and-color-space-conversion"></a>DirectDraw と色空間変換


## <span id="ddk_directdraw_and_color_space_conversion_gg"></span><span id="DDK_DIRECTDRAW_AND_COLOR_SPACE_CONVERSION_GG"></span>


DirectDraw は、サーフェスが作成され、YUV 形式で保存できます。 次の 4 つの文字コード (*Fourcc*) 色空間変換が使用されているかを示します。 次に、オーバーレイ プロセス中には、イメージは RGB の 16 ビットに変換されます。 YUV 4:2:2 は、16 ビット/ピクセル (bpp) の密度と同じでは実質的には、色の忠実性をお勧めします。 イメージは、YUV として記述でき、RGB、としてメモリを表示しますが、通常、変換、圧縮を維持するため表示メモリから読み取られるに移動します。 これにより、表示のメモリを節約し、再生速度が向上します。 Windows 2000 以降、いくつかの YUV が書式設定 (UYVY と YUY2 âˆ' 4 の両方の種類: 2:2) は、エミュレートされたが、テクスチャとして使用する場合のみです。 システム メモリ内でサポートされていない YUV 形式のサーフェスを作成できないことに注意してください。

次の 3 つの一般的な YUV 色空間は次のとおりです。

-   4:2:2 (標準的なテレビでは、この型の)

-   4:1:1 (より圧縮)

-   4:4:4 (RGB に似ています)

今すぐこれらの色空間の多くの種類と使用中の他の多くの YUV 形式があります。 FOURCC についてを参照してください、 [FOURCC](https://go.microsoft.com/fwlink/p/?linkid=8697) web サイト。

 

 





