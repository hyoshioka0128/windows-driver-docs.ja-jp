---
title: DVD 352 幅の例
description: DVD 352 幅の例
ms.assetid: 22047c8e-30e3-4204-9f7d-b8b97be668ae
keywords:
- アルファ ブレンド組み合わせ WDK DirectX va なので、DVD 352 全体の例
- ブレンド画像 WDK DirectX va なので、DVD 352 全体の例
- DVD 352 全体例 WDK DirectX VA
- WDK DirectX VA 352 全体の使用例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70453151dcb33539955ccb5bdf2050cf6f568001
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360379"
---
# <a name="dvd-352-wide-example"></a>DVD 352 幅の例


## <span id="ddk_dvd_352_wide_example_gg"></span><span id="DDK_DVD_352_WIDE_EXAMPLE_GG"></span>


DVD を使用して、704 の幅に拡大できます 352 全体図を使用できます、 **PictureSourceRect16thPel**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)(輝度サンプル間隔の解決策の 1/16) で構造体。

**PictureSourceRect16thPel**メンバーは、次の値と元の四角形を定義します。

-   **left** = 0

-   **適切な**= 16 X (**左** + *水平\_サイズ*) 5632 を =

**PictureDestinationRect**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)構造体を 2 つの代替のターゲットの四角形を定義します次の値。

1.  次の値が先の四角形。
    -   **左**= 8
    -   **適切な** = **左**+ (2 X*水平\_サイズ*) 712 を =

2.  次の値が先の四角形。
    -   **left** = 0
    -   **適切な**左 = + (2 X*水平\_サイズ*) 704 を =

2 番目のケースでは、四角形がで示される、 **GraphicDestinationRect**メンバーは、DXVA の\_BlendCombination 構造がシフトの画像の保存先を補正する 8 で、左にずれている場合

これら 2 つの方法の 2 つ目は、表示に使用するコピー先の領域のみを作成します。

 

 





