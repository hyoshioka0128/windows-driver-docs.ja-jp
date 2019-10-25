---
title: DVD 704 幅の非パン スキャンの例
description: DVD 704 幅の非パン スキャンの例
ms.assetid: df335e5e-4f7c-440a-88ef-00f6e0f916e2
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、DVD 704 ワイド非パンスキャンの例
- 画像のブレンド WDK DirectX VA、DVD 704 ワイド非パンスキャンの例
- DVD 704 全体の非パンスキャンの例 WDK DirectX VA
- 704全体の非パンスキャンの例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b044ca93b058c5fc3671e888cfcdb091b187bec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839726"
---
# <a name="dvd-704-wide-non-pan-scan-example"></a>DVD 704 幅の非パン スキャンの例


## <span id="ddk_dvd_704_wide_non_pan_scan_example_gg"></span><span id="DDK_DVD_704_WIDE_NON_PAN_SCAN_EXAMPLE_GG"></span>


704 wide 画像に対して DVD-ROM の MPEG-2 を使用するには、デコードされた画像の境界を超えるソースの四角形が必要です ( [mpeg 2 のパンスキャンの例](mpeg-2-pan-scan-example.md)で説明されている方法を使用している場合)。 この場合、DVD では、720の*水平\_サイズ\_* 、デコードされた画像の*横\_* 704 のサイズを超えるディスプレイが指定されています。 コピー元の四角形が、デコードされた画像の境界を超えている場合、ホストソフトウェアデコーダーは、割り当てられたソース領域の外への移動を維持し、変換先の四角形を管理して調整するために、ソースの四角形をトリミングします。トリミング。

ソース四角形は、次の値を使用して、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**PictureSourceRect16thPel**メンバー (輝度サンプル間隔解像度の1番目の) によって定義されます。

-   **左**= 0

-   **右**= 16 X (**左** + *横\_サイズ*) = 11264

画像の変換先の四角形は、次の2つの代替手段のいずれかによって、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体 (輝度サンプル間隔解像度の 1 ~ 16) の**ピクチャ destinationrect**メンバーによって定義されます。

1.  次の値を持つ四角形。
    -   **左**= (*表示\_水平\_サイズ*、ˆ '*横\_サイズ*)/2 = 8
    -   **右** = **左** + *水平\_サイズ*= 712

2.  次の値を持つ四角形。
    -   **左**= 0
    -   **右** = **左** + *水平\_サイズ*= 704

2番目のケースでは、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**GraphicDestinationRect**メンバーによって示される四角形が左に8つのサンプルで置き換えられ、移動した画像の変換先が補正されます。

この2つの方法のうち2番目の方法では、表示に使用されるコピー先の領域のみが作成されます。

 

 





