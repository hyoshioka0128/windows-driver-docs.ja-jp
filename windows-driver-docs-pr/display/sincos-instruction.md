---
title: SINCOS 命令の形式
description: SINCOS 命令の形式
ms.assetid: df9b51ef-5a9f-4222-a0be-a40d5b577f9a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2e21722699b161c6a5f365747e980fc5df4f0726
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536665"
---
# <a name="sincos-instruction-format"></a>SINCOS 命令の形式


## <span id="ddk_sincos_instruction_gg"></span><span id="DDK_SINCOS_INSTRUCTION_GG"></span>


SINCOS 命令を正弦と余弦をラジアン単位で計算します。 結果の X 成分には、cos(x); が含まれています。Y 成分には、sin (x) が含まれています。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>書式設定

[命令トークン](instruction-token.md)D3DSIO を格納している\_SINCOS します。 説明の長さは 4 です。

[変換先のパラメーター トークン](destination-parameter-token.md)、D3DSPR を使用して\_TEMP[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

最初[ソース パラメーター トークン](source-parameter-token.md)します。 レプリケート スィズル、つまり、X、Y、Z、または W のスィズル コンポーネント (または同等の R、G、B、または A) を明示的に使用する必要があります指定する必要があります。

**次のソース トークンが 3 よりも前のピクセルと頂点シェーダーのバージョンは\_0。つまり、ピクセルと頂点シェーダーのバージョン 3 の\_0 と後で、最初のソース パラメーター トークンのみが使用されます。**

D3DSPR を使用して 2 つ目のソース パラメーター トークン\_TEMP の種類を登録します。

3 番目のソース パラメーター トークン、D3DSPR を使用して\_TEMP の種類を登録します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

2 番目と 3 番目のソースは、一時的なレジスタとして使用できます。

ソースの登録ルール:

-   src1 します。 選択した\_チャネルは、Pi の間のラジアンで計測した角度と + Pi します。

-   src2 = (âˆ'1.f/(7!\*128)、âˆ'1.f/(6!\*64)、1.f/(4!\*16)、1.f/(5!\*32))。

-   src3 = (âˆ'1.f/(3!\*8)、âˆ'1.f/(2!\*8) 1.f、0.5f)。

    具体的には、src2 と src3 最後の 2 つの数値の順序付けは SINCOS マクロもピクセル シェーダー 2.0 では、対応するために選択されます。 これらの数値の逆には、ps を使用できるいくつかのカスタム ソース スィズルのいずれかをマクロの展開で使用できることを意味\_2\_0 (頂点シェーダーがある一般的なスィズルので問題はありません)。 これにより、sincos が使用されている場所に関係なく、使用する同じカスタム定数ができます。

変換先の登録ルール:

-   dest.x = cos (src1.selected\_チャネル)、dest.y = sin (src1.selected\_チャネル)、操作の後 dest.z は定義されていません。

-   追加先では、src1 として同じ登録をすることはできません。

-   変換先の書き込みマスクには、X と Y のみが許可されています。

SINCOS 命令は、8 つの命令スロットを受け取るマクロ命令です。

変換先の書き込みマスクには、X と Y のみが許可されています。

最大の絶対誤差は 0.002 です。

### <a name="span-idoperationspanspan-idoperationspanoperation"></a><span id="operation"></span><span id="OPERATION"></span>操作

Sin (x) と cos(x) Taylor シリーズを次に示します。


`(1) cos(x) = 1 - x2/2! + x4/4! - x6/6!
sin(x) = x - x3/3! + x5/5! - x7/7! = x*(1 - x2/3! + x4/5! - x6/7!)`

精度を向上させる、cos(x/2) を使用して cos(x) を計算します。

`(2) cos(x) = 1 - 2*sin(x/2)*sin(x/2)
sin(x) = 2*sin(x/2)*cos(x/2)`

(x に置き換えてください x によって再記述できます 1)/2 として。

`(3) cos(x) = 1 - x2/(2!*4) + x4/(4!*16) - x6/(6!*64)
sin(x) = x/2 - x3/(3!*8) + x5/(5!*32) - x7/(7!*128) =
= x*(0.5f - x2/(3!*8) + x4/(5!*32) - x6/(7!*128))`

ベクター形式で (3) を書き込むことができます。 ここで a、b、c、d は 2D 定数ベクトルです。

`a + x2*b + x4*c + x6*d = a+x2*(b + x2*(c + x2*d)`


SINCOS の実装を次に示します。


SRC2 は定数でなければなりません。

`(1.f/(7!*128), 1.f/(6!*64), 1.f/(4!*16), 1.f/(5!*32) )`

SRC3 は定数でなければなりません。

```cpp
(1.f/(3!*8), 1.f/(2!*8), 1.f, 0.5f )
VECTOR v1 = EvalSource(SRC1);
VECTOR v2 = EvalSource(SRC2);
VECTOR v3 = EvalSource(SRC3);
VECTOR v;
MUL v.z, v1.w, v1.w ; x*x
MAD v.xy, v.z, v2.xy, v2.wz
MAD v.xy, v.xy, v.z, v3.xy
MAD v.xy, v.xy, v.z, v3.wz ; 
```

部分的な sin(x/2) と最終的な cos(x/2):

```cpp
MUL v.x, v.x, v1.w ; sin(x/2)
MUL v.xy, v.xy, v.x ; compute sin(x/2)*sin(x/2) and sin(x/2)*cos(x/2)
ADD v.xy, v.xy, v.xy ; 2*sin(x/2)*sin(x/2) and 2*sin(x/2)*cos(x/2)
ADD v.x, -v.x, v3.z ; cos(x) and sin(x)
WriteResult(v, DST);
```

角度を範囲にマップできる場合は、アプリケーションは、任意の角度の SINCOS を計算する必要があります、-π. + 次のマクロを使用して Pi (r0.x は、元の角度を保持)。

```macro
def c0, Pi, 0.5f, 2*Pi, 1/(2*Pi)
mad r0.x, r.x, c0.w, c0.y
frc r0.x, r0.x
mad r0.x, r0.x, c0.z, -c0.x
```

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





