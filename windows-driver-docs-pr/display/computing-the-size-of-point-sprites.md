---
title: ポイントのスプライトのサイズの計算
description: ポイントのスプライトのサイズの計算
ms.assetid: f92ea8c6-f330-4625-873f-70c773c86334
keywords:
- Windows 2000 の WDK の表示、ポイントのスプライトの DirectX 8.0 リリース ノートします。
- WDK DirectX 8.0 のスプライトをポイントします。
- WDK ポイント スプライトのサイズ
- WDK DirectX 8.0 ポイントのサイズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86a96206888332e65105b63963a3bf69f17a2ede
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557853"
---
# <a name="computing-the-size-of-point-sprites"></a>ポイントのスプライトのサイズの計算


## <span id="ddk_computing_the_size_of_point_sprites_gg"></span><span id="DDK_COMPUTING_THE_SIZE_OF_POINT_SPRITES_GG"></span>


既存の D3DPT を使用してポイント スプライトをレンダリング\_ポイント プリミティブ型。 ポイントのスプライトのサイズを制御できる D3DRS の状態を表示するかは、新しい\_POINTSIZE または新しい FVF コンポーネント D3DFVF\_PSIZE します。

頂点、D3DFVF せず\_、D3DRS の現在の値、PSIZE 頂点コンポーネント\_POINTSIZE でレンダリング状態を使用する必要があります。 それ以外の場合、頂点データで指定された値を使用する必要があります。 いずれの場合も、値は、レンダリング ターゲットのピクセル単位でレンダリングされた四角形のサイズ (幅と高さ) は、浮動小数点数です。 ポイント サイズ レンダリング状態 (1.0) の既定値は、初期化中に、ドライバーに送信されます。

計算ポイント スプライトのサイズ、D3DRS の状態コントロール クランプ 2 レンダリング\_POINTSIZE\_MIN と D3DRS\_POINTSIZE\_最大です。 D3DRS によって指定されたサイズ以上にするポイントの計算されたサイズを固定する必要があります\_POINTSIZE\_MIN と no D3DRS によって指定されたサイズより大きい\_POINTSIZE\_最大です。 ポイントのスプライトのサイズは、描画状態で指定された最小値と最大サイズに固定されますのドライバーの責任になります。

ハードウェアの頂点の処理をサポートするドライバーは、ポイントのスプライトのサイズ可能性がありますもに基づいて調整される (目の領域) に目には、ポイントからの距離。 新しいレンダリング状態 D3DRS によってポイント スプライトのスケーリングが有効になっている\_POINTSCALEENABLE します。 これの値の状態を表示する場合は**TRUE**し、ポイントは、次のパラメーター、Sₛ 数式、および最大/最小の決定に従って拡大/縮小されます。 ユニットをスペースでは、この場合は、アプリケーションで指定されたポイントのサイズがカメラの表現に注意してください。 このスケーリングは、変換とライトだけをサポートするドライバーによって実行されます。

<span id="Si"></span><span id="si"></span><span id="SI"></span>S<sub>は</sub>  
ポイントのサイズを入力 (頂点ごとまたは D3DRS\_POINTSIZE)

<span id="A_B_C"></span><span id="a_b_c"></span>A、B、C  
スケール要因 D3DRS ポイント\_POINTSCALEA/B と C

<span id="Vh"></span><span id="vh"></span><span id="VH"></span>Vₕ  
ビューポートの高さ (**dwHeight** D3D フィールド\_ビューポート)

<span id="Pe____Xe__Ye__Ze_"></span><span id="pe____xe__ye__ze_"></span><span id="PE____XE__YE__ZE_"></span>Pₑ = (Xₑ、Yₑ、Zₑ)  
ポイントの監視領域の位置

<span id="De___sqrt__Xe2___Ye2___Ze2_"></span><span id="de___sqrt__xe2___ye2___ze2_"></span><span id="DE___SQRT__XE2___YE2___ZE2_"></span>De = sqrt (Xₑ² + Yₑ² Zₑ²)  
位置 (原点を注視目) に目からの距離

<span id="Ss___Vh___Si___sqrt_1__A___B_De___C__De2___"></span><span id="ss___vh___si___sqrt_1__a___b_de___c__de2___"></span><span id="SS___VH___SI___SQRT_1__A___B_DE___C__DE2___"></span>Sₛ = Vₕ \* S<sub>は</sub> \* sqrt (1/(A + B\*Dₑ + C\*(Dₑ²)))  
画面領域のポイント サイズ

<span id="Smax"></span><span id="smax"></span><span id="SMAX"></span>Smax  
**MaxPointSize** (D3DCAPS8 のメンバー) デバイスの機能

<span id="Smin"></span><span id="smin"></span><span id="SMIN"></span>Smin  
D3DRS\_POINTSIZE\_MIN

<span id="Final_screen-space_point_size_S__"></span><span id="final_screen-space_point_size_s__"></span><span id="FINAL_SCREEN-SPACE_POINT_SIZE_S__"></span>最終的な画面スペースのポイント サイズ S =  
Smax if Sₛ &gt; Smax

Smin 場合 Sₛ &lt; Smin

Sₛ それ以外の場合

スプライトをポイントするのではなく、1 つのピクセルの頂点を描画するのには、アプリケーションの必要がありますある以下の状態のセットをレンダリングに注意してください。

```cpp
SetRenderState (D3DRS_POINTSCALEENABLE, FALSE)
// All textures must be turned off.
SetTexture (0, NULL); 
SetTextureStageState(1, D3DTSS_COLOROP,  D3DTOP_DISABLE);
// The point size render state must be set to any value between 0.0-1.0
SetRenderState(D3DRS_POINTSIZE, 1.0);
// D3DRS_POINTSIZE_MIN and D3DRS_POINTSIZE_MAX
// must be set appropriately to allow
// D3DRS_POINTSIZE to be set to a value between 0.0-1.0
```

 

 





