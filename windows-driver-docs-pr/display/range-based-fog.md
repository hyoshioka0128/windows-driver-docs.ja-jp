---
title: 範囲ベースの霧
description: 範囲ベースの霧
ms.assetid: 6410dd21-bb9d-4985-a765-03898d9b5d0b
keywords:
- 範囲ベースの霧 WDK Direct3D
- WDK Direct3D をしてフォグをかける
- D3DPRASTERCAPS_FOGRANGE
- D3DRENDERSTATE_RANGEFOGENABLE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2b0df3d84dfebcdd68f0bd4d0492f0dde1be63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528098"
---
# <a name="range-based-fog"></a>範囲ベースの霧


## <span id="ddk_range_based_fog_gg"></span><span id="DDK_RANGE_BASED_FOG_GG"></span>


霧では、範囲に基づくことができます。 通常の z でまたは深さに基づく、霧オブジェクトは、ビューの横にある表示できますがしそれに向かって、ビューアーの回転に応じて、として、オブジェクトは表示されなくなります霧にその z 値が変更されるため。

ただし、霧は深さではなく範囲に基づいている場合に変わりませんビューアーをインプレースで回転として次の図に示すように。

![範囲ベースの霧を示す図](images/d3dfig26.png)

表示されているオブジェクトは、回転に関係なく、表示のままです。 これは、場所オブジェクト消えると、ビューアーの回転との距離の遅れを持つことがないフライト シミュレータ、タンク ゲーム、およびその他のアプリケーションの説得力のあります。

範囲に基づく霧 D3DPRASTERCAPS を設定する\_FOGRANGE と、D3DRENDERSTATE\_RANGEFOGENABLE でレンダリング状態を設定する必要があります。 これは、レンダリング D3DVERTEX 頂点のみを状態処理です。 D3DLVERTEX または D3DTLVERTEX の頂点を指定する場合、アプリケーションの RGBF フォグ値 F (霧) コンポーネントが既に範囲の修正されます。 D3DVERTEX、D3DLVERTEX、および D3DTLVERTEX 構造体は、Direct3D SDK のドキュメントで定義されます。

 

 





