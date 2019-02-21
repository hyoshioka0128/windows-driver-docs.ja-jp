---
title: テクスチャのアドレス指定およびフィルター処理
description: テクスチャのアドレス指定およびフィルター処理
ms.assetid: d468c83e-2e9c-4e4b-885e-0427714dd8a3
keywords:
- 複数のテクスチャ WDK の Direct3D のアドレス指定
- 複数のテクスチャ WDK の Direct3D のフィルター処理
- 複数のテクスチャ WDK の Direct3D のブレンド
- WDK Direct3D のブレンド
- 管理 WDK の Direct3D テクスチャのアドレス指定
- 管理 WDK の Direct3D テクスチャ フィルタ リング
- 管理 WDK の Direct3D テクスチャのブレンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209bd66b2de11c79d532f36ca089ad995c572f17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532868"
---
# <a name="texture-addressing-and-filtering-operations"></a>テクスチャのアドレス指定およびフィルター処理


## <span id="ddk_texture_addressing_and_filtering_operations_gg"></span><span id="DDK_TEXTURE_ADDRESSING_AND_FILTERING_OPERATIONS_GG"></span>


Direct3d では、という別の論理単位でテクスチャのアドレス指定、フィルター、および描画操作を実行します。、[テクスチャのステージ](texture-stages.md)します。 アドレス指定とフィルター操作はここでは説明が形成される論理的な描画操作の独立しました。 テクスチャの操作については、DirectX sdk で D3DTEXTUREOP 列挙型を参照してください。

描画の DirectX 6.0 とそれ以降のバージョンの操作と組み合わせてでは、アドレス指定して、サンプリング操作が定義されている、DirectX の今後のリリースでは、描画操作の独立したする可能性があります。 次の表のテクスチャ ステージの状態は、アドレス指定とフィルター、テクスチャのパイプラインの各ステージの操作のテクスチャを設定に使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTSS_ANISOTROPY</p></td>
<td align="left"><p>異方性フィルター処理率の制限を指定します。 これには、このテクスチャのサンプリング中に適用される異方性フィルター処理の最大の縦横比を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MAGFILTER</p></td>
<td align="left"><p>サンプルのテクスチャに使用するフィルターの種類を定義するはされる拡大 (つまり、1 つのテクセルが複数のレンダリング サーフェイスのピクセルに伸縮を取得する) 場合。 テクスチャの拡大を使用できるフィルターは、D3DTEXTUREMAGFILTER で列挙されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MAXMIPLEVEL</p></td>
<td align="left"><p>使用する最大の MIP マップ レベルを指定します。 それでも、このテクスチャは、いずれかが示される大きい MIP マップ レベルのサンプリングでことはありません。 したがって、最大次元数は 2<sup>MAXMIPLEVEL</sup>します。 0 は制限がないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MINFILTER</p></td>
<td align="left"><p>サンプルのテクスチャにされているときに使用されるフィルターの種類を定義します<em>縮小</em>、1 つのテクセルを最低 1 つの画面ピクセルにマップする、します。 D3DTEXTUREMINFILTER でテクスチャを縮小するために使用するフィルターが列挙されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPFILTER</p></td>
<td align="left"><p>フィルター処理の種類を定義、MIP マップのレイヤー間のサンプルを使用します。 このために使用できるフィルターは、D3DTEXTUREMIPFILTER で列挙されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MIPLEVEL</p></td>
<td align="left"><p>アプリケーションをハードウェアができないときに、MIP レベルを設定できます。 これは、MIP レベルはハードウェアによって判断された場合にオーバーライドされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPMAPLODBIAS</p></td>
<td align="left"><p>詳細 (LOD) の差の MIP マップ レベルを示す D3DVALUE です。 バイアス値は、MIP マップ レベルの計算、テクスチャ (および複数のエイリアス) に応じて増減ブラー許可に影響します。 単位は MIP レベルです。</p>
<p>現在/DCT WHQL テストには、MIP マップ LOD バイアス 3.0-3.0 範囲で動作する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_TEXCOORDINDEX</p></td>
<td align="left"><p>テクスチャの座標セットのインデックスを指定します。 この整数は、アドレス指定の単位はサンプリング元のテクスチャ座標のセットのインデックスを示します。 これらの座標は、「受信柔軟な頂点の書式 (<a href="fvf--flexible-vertex-format-.md" data-raw-source="[FVF](fvf--flexible-vertex-format-.md)">FVF</a>) 0 が 1 つ、2 番目のテクスチャ、テクスチャ座標の標準の DirectX セットでの数値の順序で頂点データ セットを調整したりします。 これにより、必要に応じて、テクスチャ座標のセットを共有するテクスチャ。</p></td>
</tr>
</tbody>
</table>

 

**注**   Direct3D に準拠するドライバーは、デバイスが反復処理するのみとで定義されている座標の数を使用できる場合でも、最大 8 つのテクスチャ座標セットを正しく解析するために必要**dwFVFCaps**します。 ドライバーは D3DTSS を使用する必要があります\_TEXCOORDINDEX テクスチャ リングに使用する右の座標を取得します。

 

 

 





