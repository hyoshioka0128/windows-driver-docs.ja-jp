---
title: サブ矩形のストレッチ
description: サブ矩形のストレッチ
ms.assetid: c8642ea4-67e9-4a15-9636-8d7efbfd8c9e
keywords:
- デインター レース WDK DirectX va なので、subrectangular 処理
- subrectangular 処理 WDK DirectX VA
- Windows 2000 の WDK の表示を拡大
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2874ddb904f8f13a8cf979f93dd2e6104dabbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376005"
---
# <a name="stretching-subrectangles"></a>サブ矩形のストレッチ


## <span id="ddk_stretching_subrectangles_gg"></span><span id="DDK_STRETCHING_SUBRECTANGLES_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

次の例では、宛先表面は 720 x 480、ターゲットの四角形の座標は、{0,0,720,480}背景色は黒一色とします。

ビデオ ストリームのソースの画面では、360 x 240 で、次のソースと宛先 subrectangles です。

-   ソースの矩形 (**rcSrc**)。 {180,120,360,240}

-   宛先矩形 (**rcDest**)。 {0,0,360,240}

1 つのサブストリームのソースの画面では、360 x 240 で、次のソースと宛先 subrectangles です。

-   ソースの矩形 (**rcSrc**)。 {0,0,180,120}

-   宛先矩形 (**rcDest**)。 {360,240,720,480}

次の図は、組み合わせデインター レース、サブストリーム合成の操作の出力を示します。

![伸縮 subrectangles を示す図](images/trgrect7.png)

 

 





