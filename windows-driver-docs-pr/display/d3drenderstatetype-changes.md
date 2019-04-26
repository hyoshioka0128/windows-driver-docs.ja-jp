---
title: D3DRENDERSTATETYPE の変更
description: D3DRENDERSTATETYPE の変更
ms.assetid: b62bc1f9-b9f1-40f1-aed1-752285adb3c4
keywords:
- 複数の行列による頂点の WDK Direct3D、D3DRENDERSTATETYPE のブレンド
- D3DRENDERSTATETYPE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b5237a7af393297708301b2e504c1112a56e616
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341118"
---
# <a name="d3drenderstatetype-changes"></a>D3DRENDERSTATETYPE の変更


## <span id="ddk_d3drenderstatetype_changes_gg"></span><span id="DDK_D3DRENDERSTATETYPE_CHANGES_GG"></span>


新しいレンダリング状態が定義されている操作をブレンド有効化と制御の複数の行列による頂点。D3DRENDERSTATE\_VERTEXBLEND、DirectX SDK のドキュメントに記載されています。 このレンダリング状態の値には、次の D3DVERTEXBLENDFLAGS 列挙子のいずれかを指定できます。

-   D3DVBLEND\_を無効にする (、D3DTRANSFORMSTATE で指定されたワールド マトリックスのみを使用して、\_ワールド変換状態)

-   D3DVBLEND\_1WEIGHT (、D3DTRANSFORMSTATE で指定された 2 つの世界のマトリックス間ブレンド\_世界と D3DTRANSFORMSTATE\_WORLD1 変換状態)

-   D3DVBLEND\_2WEIGHTS (、D3DTRANSFORMSTATE で指定された 3 つの世界のマトリックス間ブレンド\_WORLD、D3DTRANSFORMSTATE\_WORLD1、および D3DTRANSFORMSTATE\_WORLD2 変換状態)

-   D3DVBLEND\_3WEIGHTS (、D3DTRANSFORMSTATE で指定された 4 つのワールド行列間ブレンド\_WORLD、D3DTRANSFORMSTATE\_WORLD1、D3DTRANSFORMSTATE\_WORLD2、および D3DTRANSFORMSTATE\_WORLD3 変換状態)

については、D3DTRANSFORMSTATE\_WORLD *n*変換の状態には、D3DTRANSFORMSTATETYPE DirectX SDK のドキュメントを参照してください。

追加のブレンド ワールド行列で定義されている場合でも、 **IDirect3DDevice7::SetTransform** (Direct3D SDK のドキュメントで説明)、メソッドの外の任意の行列の投稿 (つまり、重み)、このレンダリング状態で指定した数値が 0 に設定します。

 

 





