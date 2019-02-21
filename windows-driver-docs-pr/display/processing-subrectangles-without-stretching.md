---
title: 拡張せず Subrectangles の処理
description: 拡張せず Subrectangles の処理
ms.assetid: ee59b06c-a3fb-41ac-875e-754d20a5eaa6
keywords:
- デインター レース WDK DirectX va なので、subrectangular 処理
- subrectangular 処理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82740d69a5af194bbd2feca611988b2205e41a6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560586"
---
# <a name="processing-subrectangles-without-stretching"></a>拡張せず Subrectangles の処理


## <span id="ddk_processing_subrectangles_without_stretching_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_WITHOUT_STRETCHING_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

次の 2 つの例では、宛先表面は 720 x 576、ターゲットの四角形の座標は、{0,0,720,576}背景色は黒一色とします。

最初の例でビデオ ストリームとサブストリームの四角形が交差していないケースを示します。

この例で、参照ビデオ ストリームと 1 つのサブストリームが次の四角形の座標によって特徴付けられます。

-   ビデオ ストリームの座標。
    -   ソース画面: {0,0,720,480}
    -   ソースの矩形 (**rcSrc**)。 {360,240,720,480}
    -   宛先矩形 (**rcDest**)。 {0,0,360,240}
-   サブストリームの座標。
    -   ソース画面: {0,0,640,576}
    -   ソースの矩形 (**rcSrc**)。 {0,288,320,576}
    -   宛先矩形 (**rcDest**)。 {400,0,720,288}

この例で、ビデオ ストリームの左下隅が転送先のサーフェイスの左上隅に表示され、サブストリームの右下隅が宛先表面の右上隅に表示されます。 次の図は、(ハッシュされたリージョンは、処理される subrectangles を示す) の組み合わせデインター レース、サブストリームの複合操作の出力を示します。

![積集合せず処理 subrectangles を示す図](images/trgrect5.png)

2 番目の例では、ビデオ ストリームとサブストリームの四角形が交差するケースを示します。

2 番目の例では、元の画面座標は、最初の例のように同じです。 この例で、参照ビデオ ストリームと 1 つのサブストリームが次 subrectangular 座標によって特徴付けられます。

-   ビデオ ストリーム subrectangular 座標。
    -   ソースの矩形 (**rcSrc**)。 {260,92,720,480}
    -   宛先矩形 (**rcDest**)。 {0,0,460,388}
-   サブストリーム subrectangular 座標。
    -   ソースの矩形 (**rcSrc**)。 {0,0,460,388}
    -   宛先矩形 (**rcDest**)。 {260,188,720,576}

転送先のサーフェイスの左上隅に表示されるこの例では、ビデオ ストリームの右上隅にある +100 された X と Y 軸上だけシフトします。 サブストリームの左上隅にあるが転送先のサーフェイスの右下隅に表示される-100 された X と Y 軸上だけシフトします。 次の図は、組み合わせデインター レース、サブストリーム合成の操作の出力を示します。

![積集合を処理 subrectangles を示す図](images/trgrect6.png)

 

 





