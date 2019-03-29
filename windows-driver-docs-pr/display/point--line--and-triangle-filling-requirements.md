---
title: 点、線、および三角形の塗りつぶし要件
description: 点、線、および三角形の塗りつぶし要件
ms.assetid: 1a0a8160-01e2-4fb7-b1a2-6b61f1021fb9
keywords:
- 塗りつぶしルール WDK Direct3D をポイントします。
- WDK Direct3D 線の塗りつぶしのルール
- 三角形の塗りつぶし規則 WDK Direct3D
- WDK Direct3D の行の入力
- いっぱいになるポイント WDK Direct3D
- WDK Direct3D の三角形の入力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c812aa82f357bd87c4c185a4434947205bfad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570405"
---
# <a name="point-line-and-triangle-filling-requirements"></a>点、線、および三角形の塗りつぶし要件


## <span id="ddk_point_line_and_triangle_filling_requirements_gg"></span><span id="DDK_POINT_LINE_AND_TRIANGLE_FILLING_REQUIREMENTS_GG"></span>


ポイント、線、三角形の塗りつぶしの要件は次のとおりです。

### <a name="span-idpointsspanspan-idpointsspan-points"></a><span id="points"></span><span id="POINTS"></span> ポイント

ポイントの塗りつぶしとラスタライズ規則では、ポイントを表示する方法を決定します。 これらの規則は、三角形の塗りつぶし規則と同じです。 すべてのフラグと三角形に適用する機能は、ポイント、およびその逆にも適用されます。 参照実装では、四角形へのポイントを展開し、結果に三角形の塗りつぶしルールを適用します。

4 つの新しいポイント P₁、P₂、P₃、および P₄ をように生成 P₀(x,y) の座標で指定した位置。

```cpp
P1(x,y) = (x âˆ’ 0.5, y âˆ’ 0.5)
P2(x,y) = (x âˆ’ 0.5, y + 0.5)
P3(x,y) = (x + 0.5, y + 0.5)
P4(x,y) = (x + 0.5, y âˆ’ 0.5)
```

(P₁、P₂、P₃) などの 2 つの三角形として、四角形が生成されます (P₁、P₃、P₄) とします。 ソース ファイルのレンダリングのポイントのリファレンス ラスタライザーの実装を確認することもできます。 *setup.cpp*と*scancnv.cpp*の DirectX ドライバー開発キット (DDK)。

### <a name="span-idlinesspanspan-idlinesspanlines"></a><span id="lines"></span><span id="LINES"></span>行

線の塗りつぶしルール (つまり、行を表示する方法を決定するルール) では、グリッドの交点量子化 (GIQ) 用のひし形の規則に従います。 GIQ ひし形の規則の詳細については、次を参照してください。[表面的な行](cosmetic-lines.md)します。 これらの規則を次の行を描画するコードの例はあります DirectX DDK、リファレンス ラスタライザーのソース ファイルで*setup.cpp*と*scancnv.cpp*します。

### <a name="span-idtrianglesspanspan-idtrianglesspantriangles"></a><span id="triangles"></span><span id="TRIANGLES"></span>三角形

三角形の塗りつぶし規則では、三角形のレンダリング方法を決定します。 これらの規則は、ポイントの塗りつぶしルールと同じです。 リファレンス ラスタライザーのソース ファイルで DirectX DDK の三角形の塗りつぶし規則に従った三角形を描画するコードの例を検出できます*setup.cpp*と*scancnv.cpp*します。

ハードウェアは、カリング キャップを指定およびカリングの 3 つのモードを適切に実装する必要があります。 次のコード フラグメントは、現在三角形の数を減らすかどうかを決定します。

```cpp
if (CurrentCullMode != D3DCULL_NONE) {
    int ccw = (((v[0]->sx - v[2]->sx) *
                (v[1]->sy - v[2]->sy)) <
               ((v[1]->sx - v[2]->sx) *
                (v[0]->sy - v[2]->sy)));
if ((CurrentCullMode == D3DCULL_CW && (ccw == 0)) ||
        (CurrentCullMode == D3DCULL_CCW && (ccw != 0))) {
        // Current triangle is culled, move onto
        // next triangle.
    }
}
// Current triangle is not culled, render it
```

上記はコードを三角形に接続する方法を決定するサンプルのテストです。 三角形が定義されている 0,1,2 と画面領域に反時計回りになるをテストします。 そうでない場合がありますが、時計回りにカリング時計回りの頂点になるために、その三角形が描画されていません。

 

 





