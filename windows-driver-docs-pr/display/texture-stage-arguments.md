---
title: テクスチャのステージの引数
description: テクスチャのステージの引数
ms.assetid: 434a0b88-2fb6-43e3-8a54-48f134a0dbff
keywords:
- 複数のテクスチャ WDK Direct3D テクスチャ ステージ
- WDK Direct3D のテクスチャ
- テクスチャ管理 WDK Direct3D、ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88b1fe8043c0390384b500187101280d236548b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531178"
---
# <a name="texture-stage-arguments"></a>テクスチャのステージの引数


## <span id="ddk_texture_stage_arguments_gg"></span><span id="DDK_TEXTURE_STAGE_ARGUMENTS_GG"></span>


複数のテクスチャをブレンド操作のそれぞれは、2 つの入力を結合します。 これらを呼び出すことで選択できる、 **IDirect3DDevice7::SetTextureStageState**メソッドと、D3DTEXTURESTAGESTATETYPE の次のメンバーのいずれかを指定する列挙型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列挙子</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTSS_ALPHAARG1</p></td>
<td align="left"><p>アルファの操作への最初の入力を制御します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_ALPHAARG2</p></td>
<td align="left"><p>アルファの操作に 2 番目の入力を制御します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_COLORARG1</p></td>
<td align="left"><p>色の操作への最初の入力を制御します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_COLORARG2</p></td>
<td align="left"><p>色の操作に 2 番目の入力を制御します。</p></td>
</tr>
</tbody>
</table>

 

説明については**IDirect3DDevice7::SetTextureStageState**、Direct3D SDK のドキュメントを参照してください。

### <a name="span-idtextureargumentflagsspanspan-idtextureargumentflagsspantexture-argument-flags"></a><span id="texture_argument_flags"></span><span id="TEXTURE_ARGUMENT_FLAGS"></span>テクスチャの引数のフラグ

テクスチャの各段階は、次の表のテクスチャ引数フラグを使用して上記の 4 つのパラメーターのいずれかが設定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_CURRENT</p></td>
<td align="left"><p>テクスチャの引数は、前の描画のステージの結果です。 最初のテクスチャ段階 (ステージ 0) では、この引数は、D3DTA_DIFFUSE と同じです。 これは、ことができます見なすことが、多角形の現在の色に各テクスチャのブレンドとします。 前の描画ステージ バンプ マップ テクスチャ (D3DTOP_BUMPENVMAP 操作) を使用する場合、システムはバンプ マップ テクスチャ前に、の段階からテクスチャを選択します。 (場合<em>s</em> 、現在のテクスチャのステージを表すと<em>秒 - 1</em>バンプ マップ テクスチャを含むテクスチャのステージで、この引数は結果の出力になります<em>s - 2</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_DIFFUSE</p></td>
<td align="left"><p>グーロー補間から取得した反復処理される色データ。 これは D3DTA_CURRENT テクスチャの色がその時点でないために、最初のテクスチャで ARG2 として使用多くの場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTA_TEXTURE</p></td>
<td align="left"><p>テクスチャは、このテクスチャのステージを使用してバインドされている、 <strong>IDirect3DDevice7::SetTexture</strong>(n, lpTex3) メソッド (Direct3D SDK のドキュメントで説明)、場所<em>n</em>ステージ番号です。 <strong>IDirect3DDevice7::SetTexture</strong> D3DTA_TEXTURE が引数のいずれかの場合は、このステージでは、テクスチャに使用するには、どのテクスチャ オブジェクトを定義します。 D3DTA_TEXTURE のみ D3DTSS_ALPHAARG1 と D3DTSS_COLORARG1 が含まれない D3DTSS_ALPHAARG1 と D3DTSS_COLORARG2 に存在できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_TFACTOR</p></td>
<td align="left"><p>D3DRENDERSTATE_TEXTUREFACTOR を Direct3D に設定された値。</p></td>
</tr>
</tbody>
</table>

 

**注**  一部の実装で D3DTA 両方を同時に使用されない場合があります\_TFACTOR と、D3DTA\_拡散色。

 

### <a name="span-idmodifierflagsspanspan-idmodifierflagsspanmodifier-flags"></a><span id="modifier_flags"></span><span id="MODIFIER_FLAGS"></span>修飾フラグ

次の表に示す 2 つの値は、ビットごとの OR 演算子を使用して、前のフラグのいずれかと組み合わせる必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTA_ALPHAREPLICATE</p></td>
<td align="left"><p>この引数では、そのアルファ チャネルがこの操作で使用する前にすべてのカラー チャネルにレプリケートされる場合がありますを示します。 1 つだけのコンポーネントでのテクスチャの場合は、これらの操作のすべてのカラー チャネルが自動的にレプリケートします。 ALPHA_ARGs はこのフラグを指定する必要はありませんが、それを使用しても、エラーは発生しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTA_COMPLEMENT</p></td>
<td align="left"><p>操作にこの引数を反転するかどうかを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddefaultsspanspan-iddefaultsspandefaults"></a><span id="defaults"></span><span id="DEFAULTS"></span>既定値

次の既定値は、状態は、アプリケーション塗りつぶされていない場合に使用されます。 これらの既定値は、テクスチャの複数の操作をより便利にするために定義されているときに堅牢なコードは常に完全に目的の状態を指定します。

D3DTSS\_COLORARG1 と D3DTSS\_D3DTA どちらも、既定 ALPHAARG1\_テクスチャ、対応するテクスチャが設定されている場合。 このステージでは、テクスチャが設定されていないかどうかは、これらは両方とも既定 D3DTA\_拡散します。

D3DTSS\_COLORARG2 と D3DTSS\_D3DTA ALPHAARG2 既定\_現在します。 注その D3DTA\_D3DTA 既定値は現在\_最初の段階で拡散 (D3DTA の説明で一部の例外を除き\_現在)。

ARG2 既定値は D3DTA\_拡散、ため、操作の既定値は D3DTOP は無視されますが、\_SELECTARG1 します。

D3DTA\_柔軟な頂点の書式 (FVF) データで拡散色が指定されていない場合は、既定値は 0 xfffffff を拡散します。

D3DTA\_FVF データで反射色が指定されていない場合、0x00000000 に反射が既定値します。

D3DTA\_D3DTA 既定値は現在\_場合は、前の描画ステージが、D3DTOP 場合を除いて、最初の段階を拡散\_BUMPENVMAP または D3DTOP\_BUMPENVMAPLUMINANCE 色操作。 この場合は、次が発生します。

-   場合は、前のステージが D3DTOP\_BUMPENVMAP または D3DTOP\_BUMPENVMAPLUMINANCE、し、この引数は、前のステージの前にステージの結果を示します。

-   2 番目のテクスチャ ステージ (いずれかのステージ) では、この引数の D3DTA に既定値は\_拡散します。

D3DTA\_テクスチャを D3DTSS の値は、\_COLORARG1 または D3DTSS\_ALPHAARG1 状態のいずれかの段階、または既定値は 0x0 テクスチャがこのステージにバインドされていない場合。

 

 





