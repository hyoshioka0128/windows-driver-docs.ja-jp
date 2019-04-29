---
title: 高さと幅が異なる 2 つのストリームの結合
description: 高さと幅が異なる 2 つのストリームの結合
ms.assetid: a4b0e32d-17f0-4373-bed2-ce9248b3ceb2
keywords:
- 結合は、WDK DirectX VA をストリームします。
- ビデオ ストリームが WDK DirectX VA を組み合わせる
- ストリームは、WDK DirectX VA を組み合わせる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763a1186579773c932f05f067130d6aaa0f89ee6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329857"
---
# <a name="combining-two-streams-with-different-heights-and-widths"></a>高さと幅が異なる 2 つのストリームの結合


## <span id="ddk_combining_two_streams_with_different_heights_and_widths_gg"></span><span id="DDK_COMBINING_TWO_STREAMS_WITH_DIFFERENT_HEIGHTS_AND_WIDTHS_GG"></span>


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

次の例では、VMR は、ビデオ ストリームとビデオのサブストリームの高さと幅のドライバーを呼び出します。 次の図は、方法については、この例で、ドライバーを組み合わせて、2 つのストリームと背景色を示します。

![異なる高さと幅の 2 つのストリームと背景色を組み合わせることを示す図](images/trgrect3.png)

前の例で、ドライバーの注意**DeinterlaceBltEx**関数は、のみ、次の図に示すようにターゲットの四角形を指定した背景色を描画する必要があります。

![出力画像のサイズを減らすことを示す図](images/trgrect4.png)

前の例では、2 つの要因によって水平および垂直に出力画像のサイズを小さく VMR が送られます。 背景色は、ターゲットの四角形でのみ表示する必要があります。 ドライバーをする必要があります (前の図にハッチ) ターゲットの四角形の外にある宛先表面のピクセルに書き込めません。 前の例では宛先表面は 300 x 200 ピクセルですが、ターゲットの四角形は {0, 0,150,100}。 ビデオ ストリームのソースの四角形が{0,0,300,150};、ビデオ ストリームの転送先の四角形は{0,12,150,87}します。 サブストリーム ソース四角形が{0,0,150,200}; サブストリーム先の四角形は、{37,0,112, 100}。 ターゲットの四角形は、ビデオ ストリームとすべてのサブストリームの外接する四角形であることに注意してください。

 

 





