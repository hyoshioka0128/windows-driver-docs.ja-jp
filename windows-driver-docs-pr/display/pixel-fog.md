---
title: ピクセルの不透明さ
description: ピクセルの不透明さ
ms.assetid: 40896f51-87f5-44e9-9199-e92f51a1e8f1
keywords:
- グローバル霧 WDK Direct3D
- テーブルの霧 WDK Direct3D
- ピクセル フォグ WDK Direct3D
- WDK Direct3D をしてフォグをかける
- 色霧計算 WDK Direct3D
- D3DRENDERSTATE_RANGEFOGENABLE
- D3DRENDERSTATE_FOGCOLOR
- D3DRENDERSTATE_FOGTABLEMODE
- D3DRENDERSTATE_FOGSTART
- RSTATE_FOGEND
- D3DRENDERSTATE_FOGDENSITY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6470a86c19c3c580044cee5a3099d662d2b3e6d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560358"
---
# <a name="pixel-fog"></a>ピクセルの不透明さ


## <span id="ddk_pixel_fog_gg"></span><span id="DDK_PIXEL_FOG_GG"></span>


ピクセルの不透明さは頂点の霧ブレンド係数、霧に似ています**f**、光の時刻ではなく、ラスタライズ時に計算されます。 ピクセルの不透明さは頂点フォグよりも正確です。 霧、LVERTEX で指定された要素または (Direct3D SDK のドキュメントで説明) D3DTLVERTEX 構造体のブレンドは無視されます。 ピクセルの不透明さは、次の 3 つの霧プロファイルの種類 (線形霧、指数の霧、および指数の 2 乗フォグ) に制限されます。

ピクセル フォグ ハードウェアは、各ピクセルに補間の深さの値のテーブル参照。 必要はありません 256 テーブル エントリの場合は、補間される中間直線的にします。 DirectX の今後のリリースは、非線形 z 配布用の補正を提供することができます。 間隔の値を持つ ZFront と ZBack \[0.0, 1.0\]します。

ピクセルの不透明さが設定される、 **PRIMCAPS.dwPRasterCaps** D3DPRASTERCAPS に\_FOGTABLE します。 **D3DDevice7::SetRenderState**メソッドは、設定、D3DRENDERSTATE\_FOGENABLE 表示状態を**TRUE**;、D3DRENDERSTATE\_FOGCOLOR 24 ビット rgb; の状態を表示して、D3DRENDERSTATE\_FOGTABLEMODE D3DFOG のいずれかに状態を表示する\_線形、D3DFOG\_EXP、または D3DFOG\_EXP2 します。 ここでは、ブレンド係数霧として計算されます、次の 3 つの描画状態に従って。

**fStart** D3DRENDERSTATE レンダリング状態によって決定されます\_FOGSTART が期間内と\[0.0, 1.0\]します。

**何とか**D3DRENDERSTATE レンダリング状態によって決定されます\_FOGEND が期間内と\[0.0, 1.0\]します。

**fDensity** D3DRENDERSTATE レンダリング状態によって決定されます\_FOGDENSITY が期間内と\[0.0, 1.0\]します。

霧ブレンド係数の計算**f** z 値および上記で説明した 3 つの霧描画状態に基づきます。 実際の計算は、レンダリング状態 D3DRENDERSTATE によって異なります。\_FOGTABLEMODE します。 D3DFOGMODE のみ\_線形霧の使用開始し、終了値。

-   D3DFOGMODE\_NONE

    ピクセルの不透明さは適用されません。

-   D3DFOGMODE\_線形

    線形フォグ増加します。

![線形フォグ成長の計算](images/d3dfig10.png)

-   D3DFOGMODE\_EXP

    指数フォグ増加します。

![指数フォグ成長の計算](images/d3dfig11.png)

-   D3DFOGMODE\_EXP2

    指数の 2 乗フォグ増加します。

![指数の 2 乗フォグ成長の計算](images/d3dfig12.png)

通常、指数と指数の 2 乗霧、直接実行するコストが高すぎます。 代わりに、ルックアップ テーブルは計算されて、数の z 値の間隔で\[0.0, 1.0\]現在霧密度を使用します。 最も近いテーブル エントリの現在の z 値を使用できますか、2 つの周囲の z 値間の補間の値を使用して、適切なフォグ係数を取得することができます。

最終的なフォグ色をかけます**C**頂点フォグと同じ方法で次のように計算し。

**C (f 1) =\*霧\_色 + f \* src\_色**

この数式で、

-   **f**ブレンド係数霧には

-   **霧\_色**フォグの現在の色は、(レンダリング状態 D3DRENDERSTATE によって設定\_FOGCOLOR)

-   **src\_色**が補間で、ソース テクスチャの色

場合**f**、ブレンド係数、霧は、0.0、くもり最終的な色に霧色と同じです。 場合**f** 1.0 で、フォグ効果はありません。

 

 





