---
title: Direct3D 9 の必須機能
ms.assetid: AE8ED273-2329-4E53-9FCD-5A8E863AED83
description: ユーザーモードドライバーが Direct3D 9 の機能にアクセスするために必要な機能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9586d4678596660a15ca356eab52914056064f32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825923"
---
# <a name="required-direct3d-9-capabilities"></a>Direct3D 9 の必須機能


アプリケーションが Microsoft Direct3D バージョン 9\_1、9\_2、9\_3 の機能に完全にアクセスするには、ユーザーモードドライバーが特定のハードウェア機能を公開する必要があります。 これらの機能は、ユーザーモードドライバーの[*Getcaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数によって返される[**D3DCAPS9**](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)構造体の観点から表現されます。 機能のサポートを示すために、ドライバーは、 **D3DCAPS9**のこれらのメンバーを、それぞれのフラグ値のビットごとの or に設定する必要があります。

## <a name="span-idminimum_capabilities_for_direct3d_level_9_1spanspan-idminimum_capabilities_for_direct3d_level_9_1spanspan-idminimum_capabilities_for_direct3d_level_9_1spanminimum-capabilities-for-direct3d-level-9_1"></a><span id="Minimum_capabilities_for_Direct3D_level_9_1"></span><span id="minimum_capabilities_for_direct3d_level_9_1"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_1"></span>Direct3D レベル 9\_1 の最小機能


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a>メンバー</th>
<th align="left">フラグ値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Caps2</strong></td>
<td align="left"><p>D3DCAPS2_DYNAMICTEXTURES</p>
<p>D3DCAPS2_FULLSCREENGAMMA</p></td>
</tr>
<tr class="even">
<td align="left"><strong>プレゼンテーション間隔</strong></td>
<td align="left"><p>D3DPRESENT_INTERVAL_IMMEDIATE</p>
<p>D3DPRESENT_INTERVAL_ONE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_COLORWRITEENABLE</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ShadeCaps</strong></td>
<td align="left"><p>D3DPSHADECAPS_ALPHAGOURAUDBLEND</p>
<p>D3DPSHADECAPS_COLORGOURAUDRGB</p>
<p>D3DPSHADECAPS_FOGGOURAUD</p>
<p>D3DPSHADECAPS_SPECULARGOURAUDRGB</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureFilterCaps</strong></td>
<td align="left"><p>D3DPTFILTERCAPS_MINFLINEAR</p>
<p>D3DPTFILTERCAPS_MINFPOINT</p>
<p>D3DPTFILTERCAPS_MAGFLINEAR</p>
<p>D3DPTFILTERCAPS_MAGFPOINT</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Texturecaps</strong>
<p>(以下の「メモ」を参照)。</p></td>
<td align="left"><p>D3DPTEXTURECAPS_ALPHA</p>
<p>D3DPTEXTURECAPS_CUBEMAP</p>
<p>D3DPTEXTURECAPS_MIPMAP</p>
<p>D3DPTEXTURECAPS_PERSPECTIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_CLAMP</p>
<p>D3DPTADDRESSCAPS_INDEPENDENTUV</p>
<p>D3DPTADDRESSCAPS_MIRROR</p>
<p>D3DPTADDRESSCAPS_WRAP</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TextureOpCaps</strong></td>
<td align="left"><p>D3DTEXOPCAPS_DISABLE</p>
<p>D3DTEXOPCAPS_MODULATE</p>
<p>D3DTEXOPCAPS_SELECTARG1</p>
<p>D3DTEXOPCAPS_SELECTARG2</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>SrcBlendCaps キャップ</strong></td>
<td align="left"><p>D3DPBLENDCAPS_INVDESTALPHA</p>
<p>D3DPBLENDCAPS_INVDESTCOLOR</p>
<p>D3DPBLENDCAPS_INVSRCALPHA</p>
<p>D3DPBLENDCAPS_ONE</p>
<p>D3DPBLENDCAPS_SRCALPHA</p>
<p>D3DPBLENDCAPS_ZERO</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DestBlendCaps キャップ</strong></td>
<td align="left"><p>D3DPBLENDCAPS_ONE</p>
<p>D3DPBLENDCAPS_INVSRCALPHA</p>
<p>D3DPBLENDCAPS_INVSRCCOLOR</p>
<p>D3DPBLENDCAPS_SRCALPHA</p>
<p>D3DPBLENDCAPS_ZERO</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>StretchRectFilterCaps</strong></td>
<td align="left"><p>D3DPTFILTERCAPS_MAGFLINEAR</p>
<p>D3DPTFILTERCAPS_MAGFPOINT</p>
<p>D3DPTFILTERCAPS_MINFLINEAR</p>
<p>D3DPTFILTERCAPS_MINFPOINT</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ZCmpCaps</strong></td>
<td align="left"><p>D3DPCMPCAPS_ALWAYS</p>
<p>D3DPCMPCAPS_LESSEQUAL</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>RasterCaps</strong></td>
<td align="left"><p>D3DPRASTERCAPS_DEPTHBIAS</p>
<p>D3DPRASTERCAPS_SLOPESCALEDEPTHBIAS</p></td>
</tr>
<tr class="even">
<td align="left"><strong>StencilCaps</strong></td>
<td align="left"><p>D3DSTENCILCAPS_TWOSIDED</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxSimultaneousTextures</strong></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureBlendStages</strong></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PixelShaderVersion</strong></td>
<td align="left"><p>D3DPS_VERSION (2, 0)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxPrimitiveCount</strong></td>
<td align="left"><p>65535</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexIndex</strong></td>
<td align="left"><p>65534</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVolumeExtent</strong></td>
<td align="left"><p>256</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>0、128、またはそれ以上である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>0. f</p></td>
</tr>
</tbody>
</table>

 

**メモ** 次の要件も適用されます。
-   また、ドライバーは、 **Texturecaps**メンバーを D3DPTEXTURECAPS\_NONPOW2CONDITIONAL および D3DPTEXTURECAPS\_POW2 の値、またはその両方に設定する必要があります。
-   ドライバーがイベントに応答するときに、 [**D3DDDIARG\_CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery)です。**QueryType**は、**イベントの応答**時に常に**TRUE**に設定されている必要があります。これは、イベントのが\_D3DDDIQUERYTYPE であるためです。 「 [*Createquery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)と**D3DDDIARG\_createquery**」を参照してください。

 

## <a name="span-idminimum_capabilities_for_direct3d_level_9_2spanspan-idminimum_capabilities_for_direct3d_level_9_2spanspan-idminimum_capabilities_for_direct3d_level_9_2spanminimum-capabilities-for-direct3d-level-9_2"></a><span id="Minimum_capabilities_for_Direct3D_level_9_2"></span><span id="minimum_capabilities_for_direct3d_level_9_2"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_2"></span>Direct3D レベル 9\_2 の最小機能


これらの機能は、Direct3D レベル 9\_1 に記載されているものに加えて設定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a>メンバー</th>
<th align="left">フラグ値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_SEPARATEALPHABLEND</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DevCaps2</strong></td>
<td align="left"><p>D3DDEVCAPS2_VERTEXELEMENTSCANSHARESTREAMOFFSET</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_MIRRORONCE</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Volumetexの Addresscaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_MIRRORONCE</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>2048</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>0、2048、またはそれ以上である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION (2, 0)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxPrimitiveCount</strong></td>
<td align="left"><p>1048575</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexIndex</strong></td>
<td align="left"><p>1048575</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>10000000000</p></td>
</tr>
</tbody>
</table>

 

**メモ** この要件も適用されます。
-   ドライバーが*z*検定クエリに応答する場合 ( [**D3DDDIARG\_createquery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery))。**QueryType**は D3DDDIQUERYTYPE\_オクルージョンで、応答時にクエリの**UINT**値を0以外の値に設定する必要があります。 「 [*Createquery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)と**D3DDDIARG\_createquery**」を参照してください。

 

## <a name="span-idminimum_capabilities_for_direct3d_level_9_3spanspan-idminimum_capabilities_for_direct3d_level_9_3spanspan-idminimum_capabilities_for_direct3d_level_9_3spanminimum-capabilities-for-direct3d-level-9_3"></a><span id="Minimum_capabilities_for_Direct3D_level_9_3"></span><span id="minimum_capabilities_for_direct3d_level_9_3"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_3"></span>Direct3D レベル 9\_3 の最小機能


これらの機能は、Direct3D レベル 9\_1 および 9\_2 に記載されているものに加えて設定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong></a>メンバー</th>
<th align="left">フラグ値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>キャップ</strong></td>
<td align="left"><p>D3DPS20CAPS_GRADIENTINSTRUCTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PrimitiveMiscCaps</strong></td>
<td align="left"><p>D3DPMISCCAPS_INDEPENDENTWRITEMASKS</p>
<p>D3DPMISCCAPS_MRTPOSTPIXELSHADERBLENDING</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>TextureAddressCaps</strong></td>
<td align="left"><p>D3DPTADDRESSCAPS_BORDER</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureWidth</strong></td>
<td align="left"><p>4096</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxTextureHeight</strong></td>
<td align="left"><p>4096</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxTextureRepeat</strong></td>
<td align="left"><p>0、8192、またはそれ以上である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>NumInstructionSlots</strong></td>
<td align="left"><p>512 (ピクセルシェーダーバージョン 2b)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>numtemps</strong></td>
<td align="left"><p>32 (ピクセルシェーダーバージョン 2b)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VS20Caps</strong>-&gt;<strong>numtemps</strong></td>
<td align="left"><p>32 (頂点シェーダーバージョン 2a)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexShaderConst</strong></td>
<td align="left"><p>256 (頂点シェーダーバージョン 2a)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION (3, 0) (注を参照)。</p></td>
</tr>
</tbody>
</table>

 

**メモ** D3DVS\_VERSION (3, 0) の**VertexShaderVersion**値は、インスタンス化のサポートを保証します。 Direct3D 10Level 9 では、シェーダーモデル3.0 は公開されません。

 

 

 





