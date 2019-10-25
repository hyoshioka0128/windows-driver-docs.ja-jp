---
title: 頂点バッファーのデータ形式の決定
description: 頂点バッファーのデータ形式の決定
ms.assetid: e10604f9-e800-40ff-a0e1-0f9389340e9c
keywords:
- 頂点形式 WDK Direct3D
- 柔軟な頂点形式 WDK Direct3D
- FVF WDK Direct3D
- 頂点バッファー WDK Direct3D
- Direct3D WDK Windows 2000 display、フレキシブル頂点形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6887eb9a6165eca11d3596f3eaa253271a437223
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839752"
---
# <a name="determining-the-vertex-buffer-data-format"></a>頂点バッファーのデータ形式の決定


## <span id="ddk_determining_the_vertex_buffer_data_format_gg"></span><span id="DDK_DETERMINING_THE_VERTEX_BUFFER_DATA_FORMAT_GG"></span>


頂点バッファー内のデータの形式を識別するには、ドライバーが次の情報を確認する必要があります。

-   テクスチャの次元 (1D、2D、3D、または 4D)

-   FVF データに存在するコンポーネント

-   存在するコンポーネントの順序

### <a name="span-idfvf_texture_dimensionspanspan-idfvf_texture_dimensionspanfvf-texture-dimension"></a><span id="fvf_texture_dimension"></span><span id="FVF_TEXTURE_DIMENSION"></span>FVF テクスチャディメンション

ドライバーは、DirectX SDK ドキュメントに記載されている D3DTEXTURETRANSFORMFLAGS テクスチャ座標カウントフラグ (D3DTTFF\_COUNT *n*) からテクスチャの次元を決定する必要があります。 カウントフラグの番号は、存在するテクスチャ座標の数を示します。 次のセクションで説明するように、これは必ずしもテクスチャ自体のディメンションと同じではないことに注意してください。

### <a name="span-idnonprojected_texturesspanspan-idnonprojected_texturesspannonprojected-textures"></a><span id="nonprojected_textures"></span><span id="NONPROJECTED_TEXTURES"></span>投影なしのテクスチャ

投影されていないテクスチャの一覧を次に示します。

-   D3DTTFF\_COUNT1 は、ラスタライザーが1D のテクスチャ座標を期待する必要があることを示します。

-   D3DTTFF\_COUNT2 は、ラスタライザーが2D テクスチャ座標を想定している必要があることを示します。

-   D3DTTFF\_COUNT3 は、ラスタライザーが3D テクスチャ座標を期待する必要があることを示します。

-   D3DTTFF\_COUNT4 は、ラスタライザーが4D テクスチャ座標を期待する必要があることを示します。

### <a name="span-idprojected_texturesspanspan-idprojected_texturesspanprojected-textures"></a><span id="projected_textures"></span><span id="PROJECTED_TEXTURES"></span>投影テクスチャ

予想されるテクスチャが使用されている場合、テクスチャ座標をテクスチャ座標セットの最後の (COUNT<sup>番目</sup>の) 要素で割ることを示すために、D3DTTFF\_の射影フラグが設定されます。 したがって、2D の射影テクスチャでは、最初の2つの要素が3番目の要素に分割されるため、カウントは3になります。その結果、2つの浮動小数点が参照されます。 つまり、D3DTTFF\_COUNT2 と D3DTTFF\_COUNT3 | の両方があります。D3DTTFF\_は、2D テクスチャを参照しています。

### <a name="span-idddk_fvf_vertex_data_components_ggspanspan-idddk_fvf_vertex_data_components_ggspanfvf-vertex-data-components"></a><span id="ddk_fvf_vertex_data_components_gg"></span><span id="DDK_FVF_VERTEX_DATA_COMPONENTS_GG"></span>FVF 頂点データコンポーネント

ドライバーは、 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の**Dwvertextype**メンバーに指定されているフラグを分析することによって、どのコンポーネントが存在するかを判断します。 次の表は、 **Dwvertextype**で設定できるビットフィールドと、それらが識別するコンポーネントを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DFVF_DIFFUSE</p></td>
<td align="left"><p>各頂点には拡散色があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_SPECULAR</p></td>
<td align="left"><p>各頂点には反射色があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX0</p></td>
<td align="left"><p>頂点データにはテクスチャ座標が指定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX1</p></td>
<td align="left"><p>各頂点には、テクスチャ座標のセットが1つあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX2</p></td>
<td align="left"><p>各頂点には、2つのテクスチャ座標のセットがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX3</p></td>
<td align="left"><p>各頂点には、3つのテクスチャ座標のセットがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX4</p></td>
<td align="left"><p>各頂点には、4つのテクスチャ座標のセットがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX5</p></td>
<td align="left"><p>各頂点には、5つのテクスチャ座標のセットがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX6</p></td>
<td align="left"><p>各頂点には、6組のテクスチャ座標があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX7</p></td>
<td align="left"><p>各頂点には、7つのテクスチャ座標のセットがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX8</p></td>
<td align="left"><p>各頂点には、8セットのテクスチャ座標があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_XYZRHW</p></td>
<td align="left"><p>各頂点には、 <em>x、y、z</em>、および<em>w</em>の各座標があります。</p></td>
</tr>
</tbody>
</table>

 

D3DFVF\_TEX *n*フラグのいずれか1つだけが設定されています。

### <a name="span-idddk_fvf_vertex_component_ordering_ggspanspan-idddk_fvf_vertex_component_ordering_ggspanfvf-vertex-component-ordering"></a><span id="ddk_fvf_vertex_component_ordering_gg"></span><span id="DDK_FVF_VERTEX_COMPONENT_ORDERING_GG"></span>FVF 頂点コンポーネントの順序付け

Microsoft Direct3D は、次の図に示すように、コンポーネントが順序付けされた頂点データをドライバーに提供します。

![フレキシブル頂点形式 (fvf) の頂点コンポーネントの順序付けを示す図](images/fvf.png)

Direct3D は常に*x、y、z、* および*w*の値を送信します。残りのデータは、アプリケーションによって要求された場合にのみ送信されます。 この図は、2D テクスチャ座標を前提としていますが、最新の DirectX リリースでも、1D テクスチャと4D テクスチャが有効であることに注意してください。

上の図に示すように、頂点データは次のコンポーネントで構成されています。

1.  場所 (*x、y、z、w*) (必須)

    最初の頂点コンポーネントは、頂点の位置を識別する4つの D3DVALUEs です。 Direct3D は、常に**Dwvertextype**の D3DFVF\_XYZRHW ビットを設定します。

2.  拡散色 (オプション)。

    存在する場合、このコンポーネントは、この頂点の拡散色を指定する D3DCOLOR 値です。 このコンポーネントが存在する場合、Direct3D は**Dwvertextype**の D3DFVF\_拡散ビットを設定します。

3.  反射色 (省略可能)。

    存在する場合、このコンポーネントは、この頂点の反射色を指定する D3DCOLOR 値です。 このコンポーネントが存在する場合、Direct3D は、 **Dwvertextype**の D3DFVF\_スペキュラビットを設定します。

4.  テクスチャデータ (省略可能)。

    この部分は、テクスチャの次元によって異なります。 テクスチャの各次元について、D3DVALUE は、 *u*、 *v*、 *w*、または*q*の各コンポーネントを指定します (「FVF テクスチャディメンションの説明」を参照してください)。 たとえば、2D のプロジェクションされていないテクスチャが使用されている場合、テクスチャごとに2つの D3DVALUEs が必要になります。これにより、各テクスチャの最大8個のテクスチャに対して、頂点の*u、v*の値が指定されます。 *U、v*のペアの数は*n*です。ここで、 *n*は**DWVERTEXTYPE**で設定された D3DFVF\_TEX*n*フラグに相当します。 たとえば、D3DFVF\_TEX3 が**Dwvertextype**で設定されている場合、各頂点には3つの*u、v*のペアが指定されます。

FVF データは常に厳密にパックされます。つまり、頂点バッファーに明示的に指定されていないコンポーネントでは、メモリは無駄になりません。 たとえば、 **Dwvertextype**が (D3DFVF\_XYZRHW | の場合、D3DFVF\_TEX2)、テクスチャディメンションは2D、バッファー内の各頂点は、厳密にパックされた8つの D3DVALUEs で構成されます。 次の図に示すように、2つのテクスチャ (tu ₀、tv ₀、tu ₁、tv ₁) の場所 (*x、y、z、w*) とテクスチャ座標を指定します。

![2つのテクスチャの位置とテクスチャ座標を示す図](images/vbuf.png)

上の図では、テクスチャ座標が2つだけであると想定しています。 ドライバーに渡される頂点データは、常に変換され、点灯します。 ドライバーは、法線を受信しません。 FVF テクスチャの座標セット内のすべてのデータは、単精度 IEEE 浮動小数点数です。 実装の詳細については、 *Perm3*サンプルドライバーを参照してください。 FVF の詳細については、DirectX SDK のドキュメントを参照してください。

> [!NOTE] 
> Microsoft Windows Driver Kit (WDK) には、3Dlabs Permedia3 sample display Driver (*Perm3*) が含まれていません。 このサンプルドライバーは、Windows Server 2003 SP1 Driver Development Kit (DDK) から入手できます。このドライバーは、WDHC web サイトの DDK-Windows Driver Development Kit ページからダウンロードできます。
