---
title: 頂点フォグ
description: 頂点フォグ
ms.assetid: 55083ccb-b93e-4506-baf2-358f90e2c6a6
keywords:
- 頂点フォグ WDK Direct3D
- 反復処理される霧 WDK Direct3D
- ローカル霧 WDK Direct3D
- WDK Direct3D をしてフォグをかける
- D3DRENDERSTATE_FOGENABLE
- パースペクティブに正しい霧 WDK Direct3D
- 大気モデル WDK Direct3D を階層化
- 色霧計算 WDK Direct3D
- D3DPRASTERCAPS_FOGVERTEX
- D3DRENDERSTATE_FOGDENSITY
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_SHADEMODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6696a374f48089573141d3084203284d5dea6c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387430"
---
# <a name="vertex-fog"></a>頂点フォグ


## <span id="ddk_vertex_fog_gg"></span><span id="DDK_VERTEX_FOG_GG"></span>


頂点フォグは、D3DRENDERSTATE を使用して有効になっている\_FOGENABLE が状態を表示します。 パースペクティブに正しい霧の頂点を作成できます。 ポリゴンの大きなシーンは、頂点は遠く離れているために、頂点フォグ可能性があります最適をできません。

頂点の不透明さは、2 つの方法で使用できます。

1.  作成のブレンド係数霧を定義する (Direct3D SDK のドキュメントで説明) D3DVERTEX 構造体を使用して、Direct3D 照明コードを使用します。

2.  ように D3DLVERTEX または D3DTLVERTEX 構造体の (両方が、Direct3D SDK のドキュメントで説明) を使用します。 これは、複数層の霧、霧の範囲に基づくボリューム霧などのカスタム霧効果を行うために便利です。

霧 D3DVERTEX 構造体を使用すると**PRIMCAPS.dwRasterCaps**が、D3DPRASTERCAPS\_FOGVERTEX フラグを設定します。 個々 の呼び出し、 **IDirect3DDevice7::SetRenderState** D3DRENDERSTATE を設定するメソッドを使用\_に FOGENABLE **TRUE**、および D3DRENDERSTATE\_24 ビット rgb FOGCOLOR色。 線形の霧の**IDirect3DDevice7::SetRenderState** D3DRENDERSTATE を設定するメソッドが使用される\_FOGSTART と D3DRENDERSTATE\_FOGEND します。 指数と指数乗フォグ、D3DRENDERSTATE の\_D3DLIGHTSTATETYPE で FOGDENSITY でレンダリング状態が設定されます。 詳細については、Direct3D SDK のドキュメントを参照してください。

霧 D3DTLVERTEX 構造体を使用すると、 **IDirect3DDevice7::SetRenderState** D3DRENDERSTATE を設定するメソッドを使用\_に FOGENABLE **TRUE**で霧の色を設定D3DRENDERSTATE\_FOGCOLOR、D3DRENDERSTATE を設定および\_D3DFOG に FOGTABLEMODE\_NONE (D3DTLVERTEX 構造体自体で設定されます)。 霧のブレンド係数**f**各頂点で定義されます。 これは、反射 RGBA のアルファ コンポーネントです。

次の図は、階層型大気モデルでの高度と霧の密度に関係するサンプルを示します。

![大気複数層モデルで高度と霧密度の間のサンプルの関係を示す図](images/d3dfig25.png)

ブレンド係数霧を使用して、照明フェーズ中に計算されます、頂点で反射色の値のアルファ コンポーネントに配置されます。 これによって、D3DRENDERSTATE を設定する現在の網掛けモードに従って、挿入する必要があります\_SHADEMODE が状態を表示します。

頂点 v1 の要因をブレンド霧、v2 と v3 は、次の計算を使用して決定されます。

![頂点 v1、v2 および v3 の霧ブレンド要因を示す計算](images/d3dfig8.png)

現在の網掛けモードに基づいて、三角形の間では、f1、f2、f3 が補間されます。

新しい色、 **C**、次の数式から取得されます。

**C (f 1) =\*霧\_色 + f \* src\_色**

この数式で、

-   **f**はソースの挿入の霧ブレンド係数

-   **霧\_色**フォグの現在の色は、(レンダリング状態 D3DRENDERSTATE によって設定\_FOGCOLOR)

-   **src\_色**が補間で、ソース テクスチャの色

場合**f**、ブレンド係数、霧は 0.0、 **C**霧色と等しい値に設定されます。 場合**f**は 1.0 フォグ効果はありません。

頂点でフォグ係数は、頂点には、カメラの位置からの距離の機能です。 この距離は、カメラの領域で唯一の Z 値を取得して近似でした。 コンピューティングしましたフォグの頂点ごとの (X<sub>c</sub>、Y<sub>c</sub>、Z<sub>c</sub>) カメラを使用して、頂点変換によって空間**Mworld\*Mview**頂点までの距離を計算します。

RGB モードで要素をフォグ**f** 0 ~ 255 の範囲内で指定するようにスケールし、反射の出力の色のアルファ コンポーネントに書き込まれます。

ごとの傾斜増加のモードで拡散およびスペキュラ コンポーネントがフォグ係数で乗算されて**f**し、0.0 ~ 1.0 の範囲にクランプされます。

 

 





