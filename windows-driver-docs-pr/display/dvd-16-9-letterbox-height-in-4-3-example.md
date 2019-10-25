---
title: 4 3 の DVD 16 9 レターレターの高さ (例)
description: 4 3 の DVD 16 9 レターレターの高さ (例)
ms.assetid: 67e5e50e-5102-4392-9430-feddc9609f2e
keywords:
- アルファブレンドの組み合わせ WDK DirectX VA、DVD 16 9 レターレターの高さの例
- 画像のブレンド WDK DirectX VA、DVD 16 9 レターレターの高さの例
- DVD 16 9 レターレターの高さの例 WDK DirectX VA
- 16 9 レターレターの高さの例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf8fd4c6a70c060f4e9e8125ee18b5024f45ea61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838981"
---
# <a name="dvd-169-letterbox-height-in-43-example"></a>4:3 ディスプレイでの DVD 16:9 レターボックスの高さの例


## <span id="ddk_dvd_16_9_letterbox_height_in_4_3_example_gg"></span><span id="DDK_DVD_16_9_LETTERBOX_HEIGHT_IN_4_3_EXAMPLE_GG"></span>


4:3 用の16:9 ビデオを使用すると、DVD 用のレターレターフレームが表示され、変換元と変換先の画像に対して次の値が表示されます。

次の四角形の値は、ソース画像の[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の**PictureSourceRect16thPel**メンバーで使用されます。

-   **top** = 0

-   **下** = **上**+ (16 X*縦\_サイズ*) = 7680 または9216

次の四角形の値は、変換先の画像の[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)構造体の Picture **destinationrect**メンバーで使用されます。

-   **上** = *垂直\_サイズ*/8 = 60 または72

-   **下**= 7 X*垂直\_サイズ*/8 = 420 または504

 

 





