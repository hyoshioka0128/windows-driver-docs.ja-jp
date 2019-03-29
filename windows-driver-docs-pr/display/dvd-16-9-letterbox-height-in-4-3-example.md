---
title: DVD 16 9 レター ボックスの高さ 4 3 での使用例
description: DVD 16 9 レター ボックスの高さ 4 3 での使用例
ms.assetid: 67e5e50e-5102-4392-9430-feddc9609f2e
keywords:
- アルファ ブレンド組み合わせ WDK DirectX va なので、DVD 16 9 レター ボックスの高さの例
- ブレンド画像 WDK DirectX va なので、DVD 16 9 レター ボックスの高さの例
- DVD 16 9 レター ボックスの高さ例 WDK DirectX VA
- 16 9 レター ボックスの高さ例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64bb8a0e9f3b4533cd8cb068434f2377a9df711b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580251"
---
# <a name="dvd-169-letterbox-height-in-43-example"></a>4:3 ディスプレイでの DVD 16:9 レターボックスの高さの例


## <span id="ddk_dvd_16_9_letterbox_height_in_4_3_example_gg"></span><span id="DDK_DVD_16_9_LETTERBOX_HEIGHT_IN_4_3_EXAMPLE_GG"></span>


16:9 のビデオの DVD のレター ボックス フレームに表示する 4:3 の使用には、ソースと変換先の画像の次の値があります。

次の四角形の値で使用されます、 **PictureSourceRect16thPel**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)ソースの構造画像:

-   **上部**= 0

-   **下部にある** = **上部**+ (16 X*垂直\_サイズ*) = 7680 または 9216

次の四角形の値で使用されます、 **PictureDestinationRect**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)変換先の構造画像:

-   **上部** = *垂直\_サイズ*/8 = 60 または 72

-   **下部にある**= 7 X*垂直\_サイズ*/8 = 420 または 504

 

 





