---
title: DVD 720 幅の例
description: DVD 720 幅の例
ms.assetid: 02761bf5-afae-4f38-9178-6a721fcad84e
keywords:
- アルファ ブレンド組み合わせ WDK DirectX va なので、DVD 720 全体の例
- ブレンド画像 WDK DirectX va なので、DVD 720 全体の例
- DVD 720 全体例 WDK DirectX VA
- WDK DirectX VA 720 全体の使用例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cb407c8b9227735aa09b56bfb795e181c77b638
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380232"
---
# <a name="dvd-720-wide-example"></a>DVD 720 幅の例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


720 全体図を使用する DVD には、mpeg-2 画像ソースの四角形の値で指定されたを使用して、 **PictureSourceRect16thPel**のメンバー、 [ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination) (輝度サンプル間隔の解決策の 1/16) で次の値での構造。

-   **left** = 0

-   **適切な** = **左**+ (16 X*水平\_サイズ*) 11520 を =

一般に、次の変換先の四角形の値が使用されます。

-   **left** = 0

-   **適切な** = **左** + *水平\_サイズ*720 を =

 

 





