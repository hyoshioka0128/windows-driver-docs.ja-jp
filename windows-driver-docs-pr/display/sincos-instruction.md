---
title: SINCOS 命令形式
description: SINCOS 命令形式
ms.assetid: df9b51ef-5a9f-4222-a0be-a40d5b577f9a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 831d6b7024aff671465dad3242d3d1b395ba250e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829453"
---
# <a name="sincos-instruction-format"></a>SINCOS 命令形式


## <span id="ddk_sincos_instruction_gg"></span><span id="DDK_SINCOS_INSTRUCTION_GG"></span>


SINCOS 命令は、正弦とコサインをラジアン単位で計算します。 結果の X 要素には cos (X) が含まれます。Y コンポーネントには、sin (x) が含まれています。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>形式

D3DSIO\_SINCOS を含む[命令トークン](instruction-token.md)。 命令の長さは4です。

D3DSPR\_の一時[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を使用する[ターゲットパラメータートークン](destination-parameter-token.md)。

最初の[ソースパラメータートークン](source-parameter-token.md)。 Replicate swizzle を明示的に使用する必要があります。つまり、X、Y、Z、または W swizzle コンポーネント (または R、G、B、または同等のもの) を指定する必要があります。

**次のソーストークンは、3\_0 より前のピクセルおよび頂点シェーダーバージョン用です。つまり、ピクセルおよび頂点シェーダーバージョン 3\_0 以降では、最初のソースパラメータートークンのみが使用されます。**

D3DSPR\_の一時レジスタの種類を使用する2番目のソースパラメータートークン。

D3DSPR\_の一時レジスタの種類を使用する3番目のソースパラメータートークン。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

2番目と3番目のソースは、一時レジスタとして使用できます。

ソース登録規則:

-   src1. 選択した\_チャネルは、-Pi から + Pi までのラジアンで計測された角度です。

-   src2 = (ˆ ' 1. f/(7!\*128)、ˆ ' 1. f/(6!\*64)、1. f/(4!\*16)、1. f/(5!\*32))。

-   src3 = (ˆ ' 1. f/(3!\*8)、ˆ ' 1. f/(2!\*8)、1. f、0.5 f)。

    Src2 と src3 の最後の2つの数値の順序は、ピクセルシェーダー2.0 に対応するために特に選択されます。これには、SINCOS マクロもあります。 これらの数値を逆にすると、マクロ拡張では ps\_2\_0 (頂点シェーダーには一般的な swizzle があるため、問題はありません) で使用できるいくつかのカスタムソース swizzles のいずれかを使用できることになります。 これにより、sincos が使用されている場所に関係なく、同じカスタム定数を使用できます。

送信先の登録規則:

-   dest. x = cos (src1\_channel)、dest. y = sin (src1\_channel)、dest は命令の後に定義されていません。

-   dest を src1 と同じレジスタにすることはできません。

-   宛先の書き込みマスクに使用できるのは、X と Y だけです。

SINCOS 命令は、8つの命令スロットを受け取るマクロ命令です。

宛先の書き込みマスクに使用できるのは、X と Y だけです。

絶対エラーの最大数は0.002 です。

### <a name="span-idoperationspanspan-idoperationspanoperation"></a><span id="operation"></span><span id="OPERATION"></span>運用

次に、sin (x) と cos (x) の Taylor シリーズを示します。


`(1) cos(x) = 1 - x2/2! + x4/4! - x6/6!
sin(x) = x - x3/3! + x5/5! - x7/7! = x*(1 - x2/3! + x4/5! - x6/7!)`

精度を高めるには、cos (x/2) を使用して cos (x) を計算します。

`(2) cos(x) = 1 - 2*sin(x/2)*sin(x/2)
sin(x) = 2*sin(x/2)*cos(x/2)`

(1) は、x を x/2 に置き換えることによって、次のように書き換えることができます。

`(3) cos(x) = 1 - x2/(2!*4) + x4/(4!*16) - x6/(6!*64)
sin(x) = x/2 - x3/(3!*8) + x5/(5!*32) - x7/(7!*128) =
= x*(0.5f - x2/(3!*8) + x4/(5!*32) - x6/(7!*128))`

ベクター形式で (3) 書き込みます。 A、b、c、d は、2D の定数ベクターです。

`a + x2*b + x4*c + x6*d = a+x2*(b + x2*(c + x2*d)`


次に、SINCOS の実装を示します。


SRC2 は定数である必要があります。

`(1.f/(7!*128), 1.f/(6!*64), 1.f/(4!*16), 1.f/(5!*32) )`

SRC3 は定数である必要があります。

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

部分 sin (x/2) と最後の cos (x/2):

```cpp
MUL v.x, v.x, v1.w ; sin(x/2)
MUL v.xy, v.xy, v.x ; compute sin(x/2)*sin(x/2) and sin(x/2)*cos(x/2)
ADD v.xy, v.xy, v.xy ; 2*sin(x/2)*sin(x/2) and 2*sin(x/2)*cos(x/2)
ADD v.x, -v.x, v3.z ; cos(x) and sin(x)
WriteResult(v, DST);
```

アプリケーションで任意の角度の SINCOS を計算する必要がある場合は、次のマクロを使用して、角度を-Pi... + Pi の範囲にマップできます (r0. x は元の角度を保持します)。

```macro
def c0, Pi, 0.5f, 2*Pi, 1/(2*Pi)
mad r0.x, r.x, c0.w, c0.y
frc r0.x, r0.x
mad r0.x, r0.x, c0.z, -c0.x
```

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





