---
title: 頂点ブレンド
description: 頂点ブレンド
ms.assetid: 58e740fb-01e4-4c8c-8e44-f0c358fd621a
keywords:
- 貸出 WDK Direct3D
- 頂点の WDK Direct3D のブレンド
- Direct3D WDK Windows 2000 の表示、頂点のブレンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb2073616de6260f2a715c36739b5371958d31a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390758"
---
# <a name="vertex-blending"></a>頂点ブレンド


## <span id="ddk_vertex_blending_gg"></span><span id="DDK_VERTEX_BLENDING_GG"></span>


頂点の描画操作がサポートされている Directx の最新のリリース。 この方法で動作の頂点のブレンド: そのワールド空間の原点を基準とした特定のワールド空間におけるモデルの原点を配置することで 4 X 4 ワールド行列では、領域をモデルからオブジェクトを掛けます。 マトリックスの 1 つの部分は印刷の向きを行い、別の部分は、位置。 ワールド行列を最大 3 つ適用するには、オブジェクトをオブジェクトにわたってさまざまな重み付けで頂点を融合して「曲がって」することができますがあります。

次に、view 行列を適用すると、; 特定のビュー ポイントを基準には、空間を効率的に圧縮します。カメラと同様には、2 次元の画像に現実の世界が表示されます。

 

 





