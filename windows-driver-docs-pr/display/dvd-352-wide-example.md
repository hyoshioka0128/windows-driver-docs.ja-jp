---
title: DVD 352 幅の例
description: DVD 352 幅の例
ms.assetid: 22047c8e-30e3-4204-9f7d-b8b97be668ae
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、DVD 352 全体の例
- 画像のブレンド WDK DirectX VA、DVD 352 全体の例
- DVD 352 全体の例 WDK DirectX VA
- 352全体の例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68d550b9e68bcbd8a41f0be7fbb3a7d5049d97d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839727"
---
# <a name="dvd-352-wide-example"></a>DVD 352 幅の例


## <span id="ddk_dvd_352_wide_example_gg"></span><span id="DDK_DVD_352_WIDE_EXAMPLE_GG"></span>


DVD では352の画像を使用できます。これは、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**PictureSourceRect16thPel**メンバーを使用することによって、幅704に拡張できます (輝度サンプル間隔解像度の 1 ~ 16)。

**PictureSourceRect16thPel**メンバーは、次の値を使用してソースの四角形を定義します。

-   **左**= 0

-   **右**= 16 X (**左** + *横\_サイズ*) = 5632

[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**ピクチャ destinationrect**メンバーは、次の値を持つ2つの代替変換先の四角形を定義します。

1.  次の値を持つコピー先の四角形。
    -   **左**= 8
    -   **右** = **左**+ (2 X*横\_サイズ*) = 712

2.  次の値を持つコピー先の四角形。
    -   **左**= 0
    -   **右**= 左 + (2 X*横\_サイズ*) = 704

2番目のケースでは、DXVA\_BlendCombination 構造体の**GraphicDestinationRect**メンバーによって示される四角形は、シフトされた画像の変換先を補正するために、左に8ずつ置き換えられます。

この2つの方法のうち2番目の方法では、表示に使用されるコピー先の領域のみが作成されます。

 

 





