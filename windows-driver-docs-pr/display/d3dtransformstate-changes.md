---
title: D3DTRANSFORMSTATE の変更
description: D3DTRANSFORMSTATE の変更
ms.assetid: 30d895d5-c9c3-4994-a77b-ee9eeec6d8d8
keywords:
- 複数の行列による頂点の WDK Direct3D、D3DTRANSFORMSTATE のブレンド
- D3DTRANSFORMSTATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4819b82cfd8a751bc3dbfeeebc42f550f704048
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579972"
---
# <a name="d3dtransformstate-changes"></a>D3DTRANSFORMSTATE の変更


## <span id="ddk_d3dtransformstate_changes_gg"></span><span id="DDK_D3DTRANSFORMSTATE_CHANGES_GG"></span>


複数の行列による描画と、3 つの追加のワールド変換行列の指定も必要です。

元の世界だけでなく変換マトリックス、D3DTRANSFORMSTATE\_WORLD (として考える可能性があります"D3DTRANSFORMSTATE\_WORLD0")、D3DTRANSFORMSTATE\_ビュー、および D3DTRANSFORMSTATE\_投影法、DirectX SDK のドキュメントで説明されている、次の世界変換マトリックスがあります。

-   D3DTRANSFORMSTATE\_WORLD1、blend の 2 番目の行列

-   D3DTRANSFORMSTATE\_WORLD2、blend に 3 番目の行列

-   D3DTRANSFORMSTATE\_WORLD3、blend に 4 番目の行列

これらがない連続して列挙されること元 D3DTRANSFORMSTATE 後に注意してください。\_世界です。

行列のこの呼び出しで定義されていないが、描画が有効になっていると見なされますの既定値が単位行列。

 

 





