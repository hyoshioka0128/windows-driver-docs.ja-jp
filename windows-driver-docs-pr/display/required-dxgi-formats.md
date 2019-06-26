---
title: 必須の DXGI 形式
description: このトピックでは、そのマイクロソフトの Direct3D 機能レベルにユーザー モードのディスプレイ ドライバーの要件を示します。
ms.assetid: 1CB419B9-DD5E-492F-AAAC-CFFFDE247F7F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62aed2dd826310e43360d65109e42ae260450640
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385665"
---
# <a name="required-dxgi-formats"></a>必須の DXGI 形式


このトピックでは、そのマイクロソフトの Direct3D 機能レベルにユーザー モードのディスプレイ ドライバーの要件を示します。

最初のテーブルの最初と 2 番目の列は、すべての Direct3D 形式の型を表示し、ドライバーをサポートする必要があります。 3 番目の列は、関連するすべての Direct3D の定数値を示しています [**D3D10\_形式\_サポート**](https://docs.microsoft.com/windows/desktop/api/d3d10/ne-d3d10-d3d10_format_support)や[ **D3D11\_。形式\_サポート**](https://docs.microsoft.com/windows/desktop/api/d3d11/ne-d3d11-d3d11_format_support)列挙型、ドライバーをサポートする必要があります。 4 番目の列には、ドライバーを各形式をサポートする必要があります最小 Direct3D 機能レベルが表示されます。

2 番目のテーブルは、各列挙値の Direct3D 10Level 9 のサポートのアルゴリズムを示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">(D3DDDIFMT_ * や D3DDECLTYPE D3D9 形式<em></th>
<th align="left">D3D10 + API と同じ (DXGI_FORMAT_</em>)</th>
<th align="left">D3D10_ または D3D11_ FORMAT_SUPPORT_ * 列挙の値が必要です。</th>
<th align="left">Direct3D のレベルが必要な最小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">A32B32G32R32F または D3DDECLTYPE_FLOAT4</td>
<td align="left">R32G32B32A32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_2</p>
<p>9_3</p>
<p>9_3</p>
<p>9_2</p>
<p>9_3</p>
<p>9_3</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_FLOAT3</td>
<td align="left">R32G32B32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">A16B16G16R16F または D3DDECLTYPE_FLOAT16_4</td>
<td align="left">R16G16B16A16_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_3</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_3</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">A16B16G16R16 または D3DDECLTYPE_USHORT4N</td>
<td align="left">R16G16B16A16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left">Q16W16V16U16 または D3DDECLTYPE_SHORT4N</td>
<td align="left">R16G16B16A16_SNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_SHORT4</td>
<td align="left">R16G16B16A16_SINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">G32R32F または D3DDECLTYPE_FLOAT2</td>
<td align="left">R32G32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p>
<p>9_3</p></td>
</tr>
<tr class="even">
<td align="left">D3DDECLTYPE_UBYTE4</td>
<td align="left">R8G8B8A8_UINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">A8R8G8B8 または D3DDECLTYPE_UBYTE4N</td>
<td align="left">R8G8B8A8_UNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">R8G8B8A8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">Q8W8V8U8</td>
<td align="left">R8G8B8A8_SNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">B8G8R8A8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">X8R8G8B8</td>
<td align="left">B8G8R8X8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">A8R8G8B8</td>
<td align="left">B8G8R8A8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p>
<p>DISPLAY</p>
<p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">X8R8G8B8</td>
<td align="left">B8G8R8X8_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>BLENDABLE</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">G16R16F または D3DDECLTYPE_FLOAT16_2</td>
<td align="left">R16G16_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_3</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left">G16R16 または D3DDECLTYPE_USHORT2N</td>
<td align="left">R16G16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left">V16U16 または D3DDECLTYPE_SHORT2N</td>
<td align="left">R16G16_SNORM</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_2</p>
<p>9_2</p>
<p>9_1</p>
<p>9_2</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">D3DDECLTYPE_SHORT2</td>
<td align="left">R16G16_SINT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">R32F または D3DDECLTYPE_FLOAT1</td>
<td align="left">R32_FLOAT</td>
<td align="left"><p>IA_VERTEX_BUFFER</p>
<p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>MIP</p>
<p>MIP_AUTOGEN</p>
<p>RENDER_TARGET</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">R32_UINT</td>
<td align="left"><p>IA_INDEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">S8D24 または D24S8</td>
<td align="left">D24_UNORM_S8_UINT</td>
<td align="left"><p>TEXTURE2D</p>
<p>DEPTH_STENCIL</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">L16</td>
<td align="left">R16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p>
<p>9_2</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">R16_UINT</td>
<td align="left"><p>IA_INDEX_BUFFER</p></td>
<td align="left"><p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">D16 または D16_LOCKABLE</td>
<td align="left">D16_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>DEPTH_STENCIL</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">V8U8</td>
<td align="left">R8G8_SNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">L8</td>
<td align="left">R8_UNORM</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURE3D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">DXT1</td>
<td align="left">BC1_UNORM または BC1_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="odd">
<td align="left">DXT2</td>
<td align="left">BC2_UNORM または BC2_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
<tr class="even">
<td align="left">DXT4</td>
<td align="left">BC3_UNORM または BC3_UNORM_SRGB</td>
<td align="left"><p>TEXTURE2D</p>
<p>TEXTURECUBE</p>
<p>SHADER_LOAD</p>
<p>SHADER_SAMPLE</p>
<p>MIP</p>
<p>CPU_LOCKABLE</p></td>
<td align="left"><p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p>
<p>9_1</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">D3D10_ または D3D11_ FORMAT_SUPPORT_ * 列挙の値が必要です。</th>
<th align="left">サポートのアルゴリズムで Direct3D 10Level 9</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BACK_BUFFER_CAST</p></td>
<td align="left"><p>表示をサポートする任意の形式の場合は true と見なされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BLENDABLE</p></td>
<td align="left"><p>ない FORMATOP_NOALPHABLEND</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPU_LOCKABLE</p></td>
<td align="left"><p>想定は常に true です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DISPLAY</p></td>
<td align="left"><p>ハードコーディングします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IA_VERTEX_BUFFER</p></td>
<td align="left"><p>D3DDTCAPS_ * (注を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MIP</p></td>
<td align="left"><p>ない FORMATOP_NOTEXCOORDWRAPNORMIP</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIP_AUTOGEN</p></td>
<td align="left"><p>(注を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RENDER_TARGET</p></td>
<td align="left"><p>FORMATOP_OFFSCREEN_RENDERTARGET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHADER_LOAD</p></td>
<td align="left"><p>すべての非深度形式と見なされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SHADER_SAMPLE</p></td>
<td align="left"><p>(注を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TEXTURE2D</p></td>
<td align="left"><p>FORMATOP_TEXTURE</p></td>
</tr>
<tr class="even">
<td align="left"><p>TEXTURE3D</p></td>
<td align="left"><p>FORMATOP_VOLUMETEXTURE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TEXTURECUBE</p></td>
<td align="left"><p>FORMATOP_CUBETEXTURE</p></td>
</tr>
</tbody>
</table>

 

**注**  これら Direct3D 10Level でサポートするアルゴリズムの要件の詳細については、さらに 9。
-   IA\_頂点\_バッファーや IA\_インデックス\_D3DDEVCAPS がない場合はソフトウェアの頂点を処理することによってサポートされているバッファー形式\_HWTRANSFORMANDLIGHT 機能します。
-   TEXTURE2D 形式は、深度ステンシルの形式になることから推論することもできます。
-   シェーダーの\_サンプル形式では、ドライバーは FORMATOP をサポートする必要があります\_テクスチャ、FORMATOP\_VOLUMETEXTURE、または FORMATOP\_CUBETEXTURE、また FORMATOP を報告する必要があります\_NOFILTER します。
-   MIP の\_AUTOGEN 形式、Direct3D 10Level 9 MIP が必要ですので、独自 mip マップが生成されますが、レンダリング\_ターゲット、および TEXTURE2D ビット。

 

 

 





