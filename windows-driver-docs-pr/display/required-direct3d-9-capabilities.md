---
title: Direct3D 9 の必須機能
ms.assetid: AE8ED273-2329-4E53-9FCD-5A8E863AED83
description: Direct3D 9 へのアクセスをユーザー モード ドライバーの機能に必要な機能です。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eef9102eef5761f7f71fa2bccb8c5385002dccc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376614"
---
# <a name="required-direct3d-9-capabilities"></a>Direct3D 9 の必須機能


マイクロソフトの Direct3D のバージョン 9 の機能を完全にアクセスするアプリケーションの\_1, 9\_2、および 9\_3、ユーザー モード ドライバーは、特定のハードウェア機能を公開する必要があります。 これらの機能の観点で表される、 [ **D3DCAPS9** ](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)ユーザー モード ドライバーのによって返される構造体[ *GetCaps* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数。 機能のサポートを示すために、ドライバーがのこれらのメンバーを設定する必要があります**D3DCAPS9**の各フラグの値のすべてのビット演算 OR に。

## <a name="span-idminimumcapabilitiesfordirect3dlevel91spanspan-idminimumcapabilitiesfordirect3dlevel91spanspan-idminimumcapabilitiesfordirect3dlevel91spanminimum-capabilities-for-direct3d-level-91"></a><span id="Minimum_capabilities_for_Direct3D_level_9_1"></span><span id="minimum_capabilities_for_direct3d_level_9_1"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_1"></span>Direct3D の最低限の機能レベルの 9\_1


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>メンバー</th>
<th align="left">フラグの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Caps2</strong></td>
<td align="left"><p>D3DCAPS2_DYNAMICTEXTURES</p>
<p>D3DCAPS2_FULLSCREENGAMMA</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PresentationIntervals</strong></td>
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
<td align="left"><strong>TextureCaps</strong>
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
<td align="left"><strong>SrcBlendCaps</strong></td>
<td align="left"><p>D3DPBLENDCAPS_INVDESTALPHA</p>
<p>D3DPBLENDCAPS_INVDESTCOLOR</p>
<p>D3DPBLENDCAPS_INVSRCALPHA</p>
<p>D3DPBLENDCAPS_ONE</p>
<p>D3DPBLENDCAPS_SRCALPHA</p>
<p>D3DPBLENDCAPS_ZERO</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DestBlendCaps</strong></td>
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
<td align="left"><p>D3DPS_VERSION(2,0)</p></td>
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
<td align="left"><p>0、または 128 である必要がありますまたはそれ以上。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxAnisotropy</strong></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><strong>MaxVertexW</strong></td>
<td align="left"><p>0.f</p></td>
</tr>
</tbody>
</table>

 

**注**これらの要件も適用されます。
-   ドライバーを設定する必要がありますも、 **TextureCaps** D3DPTEXTURECAPS の値にメンバー\_NONPOW2CONDITIONAL と D3DPTEXTURECAPS\_POW2、またはどちらもします。
-   ドライバーは、イベントに応答するとき、 [ **D3DDDIARG\_CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery).**QueryType**は D3DDDIQUERYTYPE\_イベント、設定があります常に、イベントの**BOOL**値を**TRUE**の応答時にします。 参照してください[ *CreateQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)と**D3DDDIARG\_CREATEQUERY**します。

 

## <a name="span-idminimumcapabilitiesfordirect3dlevel92spanspan-idminimumcapabilitiesfordirect3dlevel92spanspan-idminimumcapabilitiesfordirect3dlevel92spanminimum-capabilities-for-direct3d-level-92"></a><span id="Minimum_capabilities_for_Direct3D_level_9_2"></span><span id="minimum_capabilities_for_direct3d_level_9_2"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_2"></span>Direct3D の最低限の機能レベルの 9\_2


Direct3D レベル 9 に記載されているこれらの機能をさらに設定する必要があります\_1。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>メンバー</th>
<th align="left">フラグの値</th>
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
<td align="left"><strong>VolumeTextureAddressCaps</strong></td>
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
<td align="left"><p>0、または 2048 にする必要がありますまたはそれ以上。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION(2,0)</p></td>
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
<td align="left"><p>10000000000.f</p></td>
</tr>
</tbody>
</table>

 

**注**この要件も適用されます。
-   ドライバーに応答するときに、 *z*-クエリのテスト場所[ **D3DDDIARG\_CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createquery).**QueryType**は D3DDDIQUERYTYPE\_オクルー ジョン、設定があります常に、クエリの**UINT**値を 0 以外の値の応答時にします。 参照してください[ *CreateQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createquery)と**D3DDDIARG\_CREATEQUERY**します。

 

## <a name="span-idminimumcapabilitiesfordirect3dlevel93spanspan-idminimumcapabilitiesfordirect3dlevel93spanspan-idminimumcapabilitiesfordirect3dlevel93spanminimum-capabilities-for-direct3d-level-93"></a><span id="Minimum_capabilities_for_Direct3D_level_9_3"></span><span id="minimum_capabilities_for_direct3d_level_9_3"></span><span id="MINIMUM_CAPABILITIES_FOR_DIRECT3D_LEVEL_9_3"></span>Direct3D の最低限の機能レベルの 9\_3


Direct3D レベル 9 に記載されているこれらの機能をさらに設定する必要があります\_1 から 9\_2。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9" data-raw-source="[&lt;strong&gt;D3DCAPS9&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/d3d9caps/ns-d3d9caps-_d3dcaps9)"><strong>D3DCAPS9</strong> </a>メンバー</th>
<th align="left">フラグの値</th>
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
<td align="left"><p>0、または、8192 を指定する必要がありますまたはそれ以上。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NumSimultaneousRTs</strong></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>NumInstructionSlots</strong></td>
<td align="left"><p>512 (ピクセル シェーダーのバージョン 2 b)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>PS20Caps</strong>-&gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (ピクセル シェーダーのバージョン 2 b)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VS20Caps</strong>-&gt;<strong>NumTemps</strong></td>
<td align="left"><p>32 (頂点シェーダーのバージョン 2 a)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>MaxVertexShaderConst</strong></td>
<td align="left"><p>256 (頂点シェーダーのバージョン 2 a)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>VertexShaderVersion</strong></td>
<td align="left"><p>D3DVS_VERSION(3,0) (注を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**注**、 **VertexShaderVersion** D3DVS @property\_VERSION(3,0) がインスタンス化のサポートが保証されます。 Direct3D 10Level 9 は、シェーダー モデル 3.0 を公開しません。

 

 

 





