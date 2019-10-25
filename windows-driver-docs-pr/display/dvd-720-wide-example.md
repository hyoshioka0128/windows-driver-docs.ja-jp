---
title: DVD 720 幅の例
description: DVD 720 幅の例
ms.assetid: 02761bf5-afae-4f38-9178-6a721fcad84e
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、DVD 720 全体の例
- 画像のブレンド WDK DirectX VA、DVD 720 全体の例
- DVD 720 全体の例 WDK DirectX VA
- 720全体の例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ca20241b9588a4a0a4fa1361487628cce21853
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838977"
---
# <a name="dvd-720-wide-example"></a>DVD 720 幅の例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


720の画像を含む DVD で MPEG-2 を使用すると、 [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造の**PictureSourceRect16thPel**メンバーによって指定された画像ソースの四角形の値が使用されます (輝度のサンプルスペースの1番目の文字)解決策) を次の値に置き換えます。

-   **左**= 0

-   **右** = **左**+ (16 X*横\_サイズ*) = 11520

一般に、次の変換先の四角形の値が使用されます。

-   **左**= 0

-   **右** = **左** + *水平\_サイズ*= 720

 

 





