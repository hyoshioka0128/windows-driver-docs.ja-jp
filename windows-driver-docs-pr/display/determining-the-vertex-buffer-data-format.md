---
title: 頂点バッファーのデータ形式の決定
description: 頂点バッファーのデータ形式の決定
ms.assetid: e10604f9-e800-40ff-a0e1-0f9389340e9c
keywords:
- 頂点形式 WDK Direct3D
- 柔軟な頂点形式 WDK Direct3D
- FVF WDK Direct3D
- 頂点バッファー WDK Direct3D
- Direct3D WDK Windows 2000 の表示、柔軟な頂点の書式設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c47237926cb89856faa121f573acb58e34cb3ca8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342456"
---
# <a name="determining-the-vertex-buffer-data-format"></a>頂点バッファーのデータ形式の決定


## <span id="ddk_determining_the_vertex_buffer_data_format_gg"></span><span id="DDK_DETERMINING_THE_VERTEX_BUFFER_DATA_FORMAT_GG"></span>


頂点バッファー内のデータの形式を識別するために、ドライバーは、次の情報を確認する必要があります。

-   テクスチャのディメンション (1 次元、2 D、3 D、または 4 D)

-   FVF データに存在するコンポーネント

-   コンポーネントの順序があります。

### <a name="span-idfvftexturedimensionspanspan-idfvftexturedimensionspanfvf-texture-dimension"></a><span id="fvf_texture_dimension"></span><span id="FVF_TEXTURE_DIMENSION"></span>FVF テクスチャのディメンション

ドライバーは D3DTEXTURETRANSFORMFLAGS テクスチャ座標の数のフラグからのテクスチャのディメンションを決定する必要があります (D3DTTFF\_カウント*n*DirectX SDK のドキュメントで説明)。 カウント フラグの番号は、テクスチャ座標の数が存在するを通知します。 次のセクションで説明したようするこの必ずしも自体、テクスチャのディメンションに注意してください。

### <a name="span-idnonprojectedtexturesspanspan-idnonprojectedtexturesspannonprojected-textures"></a><span id="nonprojected_textures"></span><span id="NONPROJECTED_TEXTURES"></span>Nonprojected テクスチャ

次の一覧の nonprojected テクスチャ:

-   D3DTTFF\_COUNT1 はラスタライザーはテクスチャ座標を 1d を想定することを示します。

-   D3DTTFF\_COUNT2 はラスタライザーは 2D テクスチャ座標を想定することを示します。

-   D3DTTFF\_COUNT3 はラスタライザーは 3D テクスチャ座標を想定することを示します。

-   D3DTTFF\_COUNT4 はラスタライザーは 4 D のテクスチャ座標を想定することを示します。

### <a name="span-idprojectedtexturesspanspan-idprojectedtexturesspanprojected-textures"></a><span id="projected_textures"></span><span id="PROJECTED_TEXTURES"></span>投影されたテクスチャ

投影されたテクスチャを使用している場合、D3DTTFF\_テクスチャ座標を最後に分割することを示す予測フラグが設定されて (カウント<sup>th</sup>) テクスチャ座標のセットの要素。 したがって、2 D の射影されたテクスチャの数は 3 に、最初の 2 つの要素が 2 つの浮動小数点値を 2 D テクスチャの検索結果として、3 番目で除算するため。 つまり、両方の D3DTTFF\_COUNT2 と D3DTTFF\_COUNT3 |D3DTTFF\_予測は、2 D テクスチャを参照します。

### <a name="span-idddkfvfvertexdatacomponentsggspanspan-idddkfvfvertexdatacomponentsggspanfvf-vertex-data-components"></a><span id="ddk_fvf_vertex_data_components_gg"></span><span id="DDK_FVF_VERTEX_DATA_COMPONENTS_GG"></span>FVF 頂点データ コンポーネント

ドライバーで指定されたフラグを分析することで、コンポーネントが存在するかを決定します、 **dwVertexType**のメンバー、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)。構造体。 次の表で設定できるビット フィールドを示します**dwVertexType**と、そのユーザーを識別するコンポーネント。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DFVF_DIFFUSE</p></td>
<td align="left"><p>各頂点は、拡散色です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_SPECULAR</p></td>
<td align="left"><p>各頂点には、反射色があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX0</p></td>
<td align="left"><p>頂点データは、テクスチャ座標は提供されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX1</p></td>
<td align="left"><p>各頂点には、テクスチャ座標の 1 つのセットがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX2</p></td>
<td align="left"><p>各頂点は、2 つのテクスチャ座標のセット。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX3</p></td>
<td align="left"><p>各頂点には、3 つのテクスチャ座標があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX4</p></td>
<td align="left"><p>各頂点は、4 つのテクスチャ座標のセットです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX5</p></td>
<td align="left"><p>各頂点は、テクスチャ座標の 5 つのセットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX6</p></td>
<td align="left"><p>各頂点は、テクスチャ座標の 6 つのセットです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX7</p></td>
<td align="left"><p>各頂点は、テクスチャ座標の 7 つのセットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX8</p></td>
<td align="left"><p>各頂点は、8 つのテクスチャ座標です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_XYZRHW</p></td>
<td align="left"><p>各頂点<em>x、y、z</em>、および<em>w</em>座標。</p></td>
</tr>
</tbody>
</table>

 

1 つだけ、D3DFVF の\_TEX *n*フラグが設定されています。

### <a name="span-idddkfvfvertexcomponentorderingggspanspan-idddkfvfvertexcomponentorderingggspanfvf-vertex-component-ordering"></a><span id="ddk_fvf_vertex_component_ordering_gg"></span><span id="DDK_FVF_VERTEX_COMPONENT_ORDERING_GG"></span>FVF 頂点コンポーネントの順序付け

マイクロソフトの Direct3D には、頂点データの構成要素を持つは、次の図に示すように順序付けのドライバーが用意されています。

![頂点の柔軟な形式 (fvf) 頂点コンポーネントの順序を示す図](images/fvf.png)

Direct3D は常に送信します*x、y、z、* と*w* ; の値のみ、残りのデータが送信されるアプリケーションで必要とします。 この図で、2 D テクスチャ座標を前提とされるに注意してください 1 D、3 D、および 4 D テクスチャも DirectX の最新のリリースで有効です。

上記の図に示すように、頂点データは、次のコンポーネントで構成されます。

1.  場所 (*x、y、z、w*) (必須)

    最初の頂点のコンポーネントは、頂点の位置を識別する 4 つの D3DVALUEs です。 Direct3D、常に設定、D3DFVF\_XYZRHW ビット**dwVertexType**します。

2.  (省略可能) の色を拡散します。

    存在する場合、このコンポーネントは、この頂点の拡散色を指定する D3DCOLOR 値です。 Direct3D の設定、D3DFVF\_ビット拡散**dwVertexType**このコンポーネントが存在する場合。

3.  反射色は (省略可能)。

    存在する場合、このコンポーネントは、この頂点の反射色を指定する D3DCOLOR 値です。 Direct3D の設定、D3DFVF\_ビット反射**dwVertexType**このコンポーネントが存在する場合。

4.  テクスチャ データ (省略可能)。

    この部分は、テクスチャのディメンションによって異なります。 テクスチャの各ディメンションに対して、D3DVALUE を指定の各、 *u*、 *v*、 *w*、または*q*コンポーネント (FVF テクスチャの説明を参照してください。ディメンションの場合)。 たとえば、nonprojected 2 D のテクスチャを使用している場合テクスチャあたり 2 つの D3DVALUEs が頂点を指定する必要は*u, v*テクスチャ合計最大 8 つのテクスチャの各値。 数*u, v*ペアの存在が*n*ここで、 *n* 、D3DFVF に対応する\_TEX*n*フラグで設定**dwVertexType**します。 たとえば場合、D3DFVF\_TEX3 設定されている**dwVertexType**し、次の 3 つ、 *u, v*ペアは、各頂点で提供されています。

FVF データは常に緊密にパックされた;つまり、頂点バッファーに明示的に指定されていないコンポーネントのメモリは消費しません。 たとえば、 **dwVertexType**は (D3DFVF\_XYZRHW |D3DFVF\_TEX2)、およびテクスチャのディメンションは、2 D、緊密にパックされた D3DVALUEs の 8 つのバッファー内の各頂点で構成されます。 これらの場所を指定 (*x、y、z、w*) および次の図に示すように、(tu₀、tv₀、tu₁、tv₁) の 2 つのテクスチャの座標をテクスチャします。

![2 つのテクスチャの場所およびテクスチャの座標を示す図](images/vbuf.png)

上記の図でテクスチャ座標の 2 つだけあると見なされます。 ドライバーに渡される頂点データは常に変換し、点灯します。 ドライバーは、法線を受信しません。 FVF テクスチャの座標セットのすべてのデータは、IEEE 単精度浮動小数点数です。 実装の詳細については、次を参照してください。、 *Perm3*サンプル ドライバー。 FVF の詳細については、DirectX SDK のドキュメントを参照してください。

> [!NOTE] 
> Microsoft Windows Driver Kit (WDK) に 3 dlabs Permedia3 サンプルのディスプレイ ドライバーが含まれていません (*Perm3.h*)。 Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできるこのサンプル ドライバーを取得できます。
