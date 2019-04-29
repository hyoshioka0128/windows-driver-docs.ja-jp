---
title: 頂点フォグとピクセル フォグ
description: 頂点フォグとピクセル フォグ
ms.assetid: 4cdba82f-0cfe-4416-951c-59b577c7f30e
keywords:
- フォグをかける WDK Direct3D ピクセル
- 頂点フォグ WDK Direct3D
- WDK Direct3D をしてフォグをかける
- 線形フォグ WDK Direct3D
- 指数霧 WDK Direct3D
- 指数 2 乗フォグ WDK Direct3D
- モノクロ照明 WDK Direct3D
- 色霧計算 WDK Direct3D
- ブレンド フォグ係数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6cb7e11cbc1802167deb8881fe0b9e2a06e4c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390785"
---
# <a name="vertex-and-pixel-fogging"></a>頂点フォグとピクセル フォグ


## <span id="ddk_vertex_and_pixel_fogging_gg"></span><span id="DDK_VERTEX_AND_PIXEL_FOGGING_GG"></span>


次の 3 つの主なプロファイルの種類: 線形、指数、および指数乗します。 2 つの主要な実装方法もあります。 頂点霧 (霧の反復処理されるか、ローカルとも呼ばれます) とピクセル霧 (テーブルまたはグローバル霧とも呼ばれます)。

モノクロ (傾斜) 照明モードで、霧は霧色は黒の場合にのみ正しく動作できます。 (光源がない場合は、霧の任意の色動作霧が黒でレンダリングされるためです。)霧は、オブジェクトの可視性--霧値が低いほど、フォグが大きいほど、および可視性の測定と見なされます。

ブレンド係数霧**f**霧のすべての計算で使用されます。 オブジェクトの色と霧色の割合を意味します。 最終的な色は、次の式によって決定されます。

**Color = f \* objColor + (1.0 - f) \* fogColor**

そのため、霧のブレンド係数の 0.0 は完全な霧色とブレンド率は 1.0 霧は完全なオブジェクトの色。 通常、 **f**距離が減少します。

次の図に示すようまでの距離が多いほど、線形フォグ密度が直線的に増加します。

![線形霧を示す図](images/d3dfig23.png)

この線形増加は、指数の霧霧密度が指数関数的に増加によって異なります。 線形フォグ プロファイルは次のように設定する可能性があります。 D3DRENDERSTATE\_ZFront に FOGSTART でレンダリング状態が設定されていると*f* = 1.0;、D3DRENDERSTATE\_ZBack に FOGEND でレンダリング状態が設定されていると*f*は 0.0。 D3DRENDERSTATE\_FOGDENSITY でレンダリング状態は無視されます。

 

 





