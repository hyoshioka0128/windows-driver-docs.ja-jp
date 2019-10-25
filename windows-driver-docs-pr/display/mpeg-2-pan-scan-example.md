---
title: MPEG-2 パンスキャンの例
description: MPEG-2 パンスキャンの例
ms.assetid: 6ce4722c-5406-4b29-9171-ecab049320e7
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、MPEG 2 パンスキャンの例
- 画像のブレンド WDK DirectX VA、MPEG 2 パンスキャンの例
- PictureSourceRect16thPel
- MPEG-2 パンスキャンの例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d91ffd7b8f5257b26163b50036a7bdcc1a276db7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840551"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 パンスキャンの例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**PictureSourceRect16thPel**メンバーを使用して、mpeg-2 ビデオパンスキャンパラメーターによって指定された領域を選択すると、 **PictureSourceRect16thPel**メンバーの値を計算できます。次の式を使用します。 **PictureSourceRect16thPel**を使用する場合、これらの値は、アルファブレンドの組み合わせバッファーに記述されている制限に違反しないようにしてください。 詳細については、DXVA\_BlendCombination 構造体の「**解説**」を参照してください。

これらの制約は、いくつかの MPEG **PictureSourceRect16thPel**のパンスキャンパラメーターで違反する可能性があります。特に、MPEG 2 DVD コンテンツによっては、一部の調整が必要になる場合があります。

-   **左**= 8 x (*横\_サイズ* - *水平方向\_サイズ\_表示*)-*フレーム\_中央\_横\_オフセット*

-   **上位**= 8 x (*縦\_サイズ-表示\_垂直\_サイズ*)-*フレーム\_中央\_垂直\_オフセット*

-   **右** = **左**+ (16 x*ディスプレイ\_横\_サイズ*)

-   **下** = **上**+ (16 x*ディスプレイ\_垂直\_サイズ*)

DXVA\_BlendCombination 構造体の**画像 Destinationrect**メンバーは、通常、次の値を使用します。

-   **左**= 0 または 8 (DVD 704 に含まれる、[非パンスキャンの画像の例](dvd-704-wide-non-pan-scan-example.md))

-   **top** = 0

-   **右** = **左** + *表示\_水平\_サイズ*

-   **下** = **上部** +  *\_垂直方向の\_のサイズを表示*します

 

 





