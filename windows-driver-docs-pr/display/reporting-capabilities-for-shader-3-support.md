---
title: Shader 3 のサポートに対するレポート機能
description: Shader 3 のサポートに対するレポート機能
ms.assetid: 89590647-646c-47ec-a46e-e781b1b9f33e
keywords:
- シェーダー WDK DirectX 9.0、シェーダー 3.0 のサポート
- 頂点シェーダー WDK DirectX 9.0、シェーダー 3.0 のサポート
- ピクセル シェーダー WDK DirectX 9.0、シェーダー 3.0 のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e57409a4ef41be2a6dc3b33fdfd3cf56e68dad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539497"
---
# <a name="reporting-capabilities-for-shader-3-support"></a>Shader 3 のサポートに対するレポート機能


## <span id="ddk_reporting_capabilities_for_shader_3_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_3_SUPPORT_GG"></span>


3.0 以降のピクセルまたは頂点シェーダーのバージョンをサポートしているディスプレイ デバイスの DirectX 9.0 バージョンのドライバーでは、次の機能をサポートしているを示す必要があります。

### <a name="span-idvertexshader30andlaterspanspan-idvertexshader30andlaterspanvertex-shader-30-and-later"></a><span id="vertex_shader_3_0_and_later"></span><span id="VERTEX_SHADER_3_0_AND_LATER"></span>3.0 以降、頂点シェーダー

デバイスは、頂点シェーダー 3.0 以降をサポートする場合、そのドライバーは、次の値に D3DCAPS9 構造体のメンバーを設定する必要があります。

<span id="VS20Caps"></span><span id="vs20caps"></span><span id="VS20CAPS"></span>**VS20Caps**  
設定は次のメンバー、D3DVSHADERCAPS2 の\_0 構造体。

**DynamicFlowControlDepth** 24 に設定します。

**NumTemps**を 32 に設定します。

**StaticFlowControlDepth** 4 に設定します。

**Cap** 、D3DVS20CAPS に設定\_を示すその predication PREDICATION ビットがサポートされています。

<span id="GuardBandLeft__GuardBandTop__GuardBandRight__GuardBandBottom"></span><span id="guardbandleft__guardbandtop__guardbandright__guardbandbottom"></span><span id="GUARDBANDLEFT__GUARDBANDTOP__GUARDBANDRIGHT__GUARDBANDBOTTOM"></span>**GuardBandLeft、GuardBandTop、GuardBandRight、GuardBandBottom**  
それぞれ 8 K を設定します。

<span id="VertexShaderVersion"></span><span id="vertexshaderversion"></span><span id="VERTEXSHADERVERSION"></span>**VertexShaderVersion**  
3.0 に設定します。

<span id="MaxVertexShaderConst"></span><span id="maxvertexshaderconst"></span><span id="MAXVERTEXSHADERCONST"></span>**MaxVertexShaderConst**  
256 に設定します。

<span id="MaxVertexShader30InstructionSlots"></span><span id="maxvertexshader30instructionslots"></span><span id="MAXVERTEXSHADER30INSTRUCTIONSLOTS"></span>**MaxVertexShader30InstructionSlots**  
512 に設定します。

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
設定、D3DPRASTERCAPS\_FOGVERTEX ビット霧サポートをします。

<span id="VertexTextureFilterCaps"></span><span id="vertextexturefiltercaps"></span><span id="VERTEXTEXTUREFILTERCAPS"></span>**VertexTextureFilterCaps**  
次のフィルター機能を設定します。

D3DPTFILTERCAPS\_MINFPOINT

D3DPTFILTERCAPS\_MAGFPOINT

<span id="DevCaps2"></span><span id="devcaps2"></span><span id="DEVCAPS2"></span>**DevCaps2**  
設定、D3DDEVCAPS2\_VERTEXELEMENTSCANSHARESTREAMOFFSET 頂点宣言内の頂点の要素が同じストリーム オフセットを共有できることを示すビットします。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
デバイスでサポートされている頂点データの種類を示す次のビットを設定します。

D3DDTCAPS\_UBYTE4

D3DDTCAPS\_UBYTE4N

D3DDTCAPS\_SHORT2N

D3DDTCAPS\_SHORT4N

D3DDTCAPS\_FLOAT16

D3DDTCAPS\_FLOAT16

### <a name="span-idpixelshader30andlaterspanspan-idpixelshader30andlaterspanpixel-shader-30-and-later"></a><span id="pixel_shader_3_0_and_later"></span><span id="PIXEL_SHADER_3_0_AND_LATER"></span>3.0 以降、ピクセル シェーダー

デバイスは、ピクセル シェーダー 3.0 以降をサポートする場合、そのドライバーは、次の値に D3DCAPS9 構造体のメンバーを設定する必要があります。

<span id="PS20Caps"></span><span id="ps20caps"></span><span id="PS20CAPS"></span>**PS20Caps**  
設定は次のメンバー、D3DPSHADERCAPS2 の\_0 構造体。

**DynamicFlowControlDepth** 24 に設定します。

**NumTemps**を 32 に設定します。

**StaticFlowControlDepth** 4 に設定します。

**NumInstructionSlots** 512 に設定します。

**Cap**以下のビットに設定します。

D3DPS20CAPS\_ARBITRARYSWIZZLE を任意のスィズルがサポートされていることを示します。

D3DPS20CAPS\_GRADIENTINSTRUCTIONS をグラデーション命令がサポートされていることを示します。

D3DPS20CAPS\_を示すその predication PREDICATION がサポートされています。

D3DPS20CAPS\_NODEPENDENTREADLIMIT 制限に読み取り依存はありません。

D3DPS20CAPS\_NOTEXINSTRUCTIONLIMIT テクスチャ、数学の手順の組み合わせに制限なしを指定します。

<span id="MaxTextureWidth__MaxTextureHeight"></span><span id="maxtexturewidth__maxtextureheight"></span><span id="MAXTEXTUREWIDTH__MAXTEXTUREHEIGHT"></span>**MaxTextureWidth、MaxTextureHeight**  
各 4 K に設定します。

<span id="MaxTextureRepeat"></span><span id="maxtexturerepeat"></span><span id="MAXTEXTUREREPEAT"></span>**MaxTextureRepeat**  
8 K に設定します。

<span id="MaxAnisotropy"></span><span id="maxanisotropy"></span><span id="MAXANISOTROPY"></span>**MaxAnisotropy**  
16 に設定します。

<span id="PixelShaderVersion"></span><span id="pixelshaderversion"></span><span id="PIXELSHADERVERSION"></span>**PixelShaderVersion**  
3.0 に設定します。

<span id="MaxPixelShader30InstructionSlots"></span><span id="maxpixelshader30instructionslots"></span><span id="MAXPIXELSHADER30INSTRUCTIONSLOTS"></span>**MaxPixelShader30InstructionSlots**  
512 に設定します。

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
次のビットを設定します。

D3DPMISCCAPS\_MASKZ

すべての選別モード:D3DPMISCCAPS\_CULLNONE、D3DPMISCCAPS\_CULLCW、D3DPMISCCAPS\_CULLCCW します。

D3DPMISCCAPS\_COLORWRITEENABLE

D3DPMISCCAPS\_CLIPPLANESCALEDPOINTS

D3DPMISCCAPS\_CLIPTLVERTS

D3DPMISCCAPS\_BLENDOP

D3DPMISCCAPS\_FOGINFVF

<span id="RasterCaps"></span><span id="rastercaps"></span><span id="RASTERCAPS"></span>**RasterCaps**  
次のビットを設定します。

D3DPRASTERCAPS\_MIPMAPLODBIAS

D3DPRASTERCAPS\_異方性

D3DPRASTERCAPS\_COLORPERSPECTIVE

D3DPRASTERCAPS\_SCISSORTEST

完全な深さのサポート:D3DPRASTERCAPS\_SLOPESCALEDEPTHBIAS、D3DPRASTERCAPS\_DEPTHBIAS

<span id="ZCmpCaps"></span><span id="zcmpcaps"></span><span id="ZCMPCAPS"></span>**ZCmpCaps**  
ステンシル、深さ、およびアルファ テストの比較の完全なセットの次のビットを設定します。

D3DPCMPCAPS\_なし

D3DPCMPCAPS\_小さい

D3DPCMPCAPS\_と等しい

D3DPCMPCAPS\_LESSEQUAL

D3DPCMPCAPS\_GREATER

D3DPCMPCAPS\_NOTEQUAL

D3DPCMPCAPS\_率は

D3DPCMPCAPS\_常に。

<span id="SrcBlendCaps__DestBlendCaps"></span><span id="srcblendcaps__destblendcaps"></span><span id="SRCBLENDCAPS__DESTBLENDCAPS"></span>**SrcBlendCaps、DestBlendCaps**  
次のソースと特記が変換先の描画モードを設定します。

D3DPBLENDCAPS\_0

D3DPBLENDCAPS\_いずれか

D3DPBLENDCAPS\_SRCCOLOR

D3DPBLENDCAPS\_INVSRCCOLOR

D3DPBLENDCAPS\_SRCALPHA

D3DPBLENDCAPS\_INVSRCALPHA

D3DPBLENDCAPS\_DESTALPHA

D3DPBLENDCAPS\_INVDESTALPHA

D3DPBLENDCAPS\_DESTCOLOR

D3DPBLENDCAPS\_INVDESTCOLOR

D3DPBLENDCAPS\_SRCALPHASAT (設定されていない**DestBlendCaps**)

D3DPBLENDCAPS\_BOTHSRCALPHA (設定されていない**DestBlendCaps**)

D3DPBLENDCAPS\_BOTHINVSRCALPHA (設定されていない**DestBlendCaps**)

D3DPBLENDCAPS\_BLENDFACTOR

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
次のテクスチャ機能を設定します。

D3DPTEXTURECAPS\_パースペクティブ

D3DPTEXTURECAPS\_TEXREPEATNOTSCALEDBYSIZE

D3DPTEXTURECAPS\_予測

D3DPTEXTURECAPS\_キューブ マップ

D3DPTEXTURECAPS\_VOLUMEMAP

D3DPTEXTURECAPS\_MIPMAP

D3DPTEXTURECAPS\_MIPVOLUMEMAP

D3DPTEXTURECAPS\_MIPCUBEMAP

<span id="TextureFilterCaps__VolumeTextureFilterCaps__CubeTextureFilterCaps"></span><span id="texturefiltercaps__volumetexturefiltercaps__cubetexturefiltercaps"></span><span id="TEXTUREFILTERCAPS__VOLUMETEXTUREFILTERCAPS__CUBETEXTUREFILTERCAPS"></span>**TextureFilterCaps、VolumeTextureFilterCaps、CubeTextureFilterCaps**  
各場合を除き、次のフィルター機能を設定します。

D3DPTFILTERCAPS\_MINFPOINT

D3DPTFILTERCAPS\_MINFLINEAR

D3DPTFILTERCAPS\_MINFANISOTROPIC (は必要ありません**VolumeTextureFilterCaps**と**CubeTextureFilterCaps**)

D3DPTFILTERCAPS\_MIPFPOINT

D3DPTFILTERCAPS\_MIPFLINEAR

D3DPTFILTERCAPS\_MAGFPOINT

D3DPTFILTERCAPS\_MAGFLINEAR

<span id="TextureAddressCaps"></span><span id="textureaddresscaps"></span><span id="TEXTUREADDRESSCAPS"></span>**TextureAddressCaps**  
次のテクスチャを頂点とピクセルの段階でのサポートを示すためにアドレス モードを設定します。

D3DPTADDRESSCAPS\_ラップ

D3DPTADDRESSCAPS\_ミラー

D3DPTADDRESSCAPS\_クランプ

D3DPTADDRESSCAPS\_罫線

D3DPTADDRESSCAPS\_INDEPENDENTUV

D3DPTADDRESSCAPS\_MIRRORONCE

<span id="StencilCaps"></span><span id="stencilcaps"></span><span id="STENCILCAPS"></span>**StencilCaps**  
ステンシル操作のサポートを示すための以下のビットを設定します。

D3DSTENCILCAPS\_保持

D3DSTENCILCAPS\_0

D3DSTENCILCAPS\_置き換えます

D3DSTENCILCAPS\_INCRSAT

D3DSTENCILCAPS\_DECRSAT

D3DSTENCILCAPS\_反転

D3DSTENCILCAPS\_INCR

D3DSTENCILCAPS\_DECR

D3DSTENCILCAPS\_TWOSIDED

<span id="FVFCaps"></span><span id="fvfcaps"></span><span id="FVFCAPS"></span>**FVFCaps**  
設定、D3DFVFCAPS\_PSIZE 機能をデバイスで頂点ごとのポイント サイズをサポートすることを示します。

<span id="TextureCaps"></span><span id="texturecaps"></span><span id="TEXTURECAPS"></span>**TextureCaps**  
デバイスが完全にサポートまたは条件付き nonpow-2 のテクスチャのサポートをサポートしていることを示します。 詳細については、次を参照してください。[シェーダー 2 のサポートの機能を Reporting](reporting-capabilities-for-shader-2-support.md)します。

必要があります**いない**設定、D3DPTEXTURECAPS\_SQUAREONLY ビット。 デバイスは、正方形のテクスチャのみに制限することはできません。

デバイスがサポートしている場合[に複数のターゲットを同時にレンダリング](rendering-to-multiple-targets-simultaneously.md)(つまり、 **NumSimultaneousRTs**メンバーが 1 より大きい値に設定されます)、そのドライバーが D3DCAPS9 構造体のメンバーを設定する必要があります、次の値。

<span id="PrimitiveMiscCaps"></span><span id="primitivemisccaps"></span><span id="PRIMITIVEMISCCAPS"></span>**PrimitiveMiscCaps**  
次のビットを設定します。

D3DPMISCCAPS\_INDEPENDENTWRITEMASKS

D3DPMISCCAPS\_MRTINDEPENDENTBITDEPTHS

D3DPMISCCAPS\_MRTPOSTPIXELSHADERBLENDING

<span id="MaxUserClipPlanes"></span><span id="maxuserclipplanes"></span><span id="MAXUSERCLIPPLANES"></span>**MaxUserClipPlanes**  
頂点シェーダー 3.0 以降がサポートされている場合は、6 に設定します。

<span id="DeclTypes"></span><span id="decltypes"></span><span id="DECLTYPES"></span>**DeclTypes**  
頂点シェーダー 3.0 以降がサポートされている場合、デバイスがサポートする頂点の書式を示す次のビットを設定します。

D3DDTCAPS\_SHORT2N

D3DDTCAPS\_SHORT4N

D3DDTCAPS\_UDEC3

D3DDTCAPS\_DEC3N

 

 





