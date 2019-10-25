---
title: ハードウェアの変革と照明
description: ハードウェアの変革と照明
ms.assetid: b45aa56e-2d8c-412a-b581-a1e2002d4fac
keywords:
- Direct3D WDK Windows 2000 display、hardware tansform、および照明
- テクスチャ変換 WDK Direct3D
- WDK Direct3D を変換します。
- 照明 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34351f12fc6e90c5fbbcc26b362777e5bacd118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838899"
---
# <a name="hardware-transform-and-lighting"></a>ハードウェアの変革と照明


## <span id="ddk_hardware_transform_and_lighting_gg"></span><span id="DDK_HARDWARE_TRANSFORM_AND_LIGHTING_GG"></span>


照明や変換などのジオメトリ操作のハードウェアの高速化が有効になり、最新の Direct X リリースの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI に変更が加えられました。 API レベルでは、ハードウェアでの頂点操作をサポートするデバイスは、ラスタライズのみを行うデバイスとは別に列挙されます。

既存の caps 構造は、ハードウェアアクセラレーションデバイス上に存在する可能性がある機能を示すように拡張されています。 たとえば、サポートされている光源の数は、 [**D3DDEVICEDESC\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)構造で報告される[**D3DLIGHTINGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dlightingcaps)構造体の**dwnumlights**メンバーで設定されます。

次の表に、その他のフラグを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_CANBLTSYSTONONLOCAL</p></td>
<td align="left"><p>デバイスは、システムメモリから非ローカルビデオメモリへのテクスチャ blt をサポートしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_DRAWPRIMITIVES2EX</p></td>
<td align="left"><p>このドライバーは、拡張<em>D3dDrawPrimitives2</em>機能をサポートすることによって、DirectX 7.0 に準拠しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_HWRASTERIZATION</p></td>
<td align="left"><p>デバイスは、ラスター化にハードウェアアクセラレータを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_HWTRANSFORMANDLIGHT</p></td>
<td align="left"><p>デバイスは、ハードウェアの変換と照明の両方をサポートできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_SEPARATETEXTUREMEMORIES</p></td>
<td align="left"><p>デバイスは、個別のメモリプールからのテクスチャを行います。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTRANSFORMCAPS_CLIP</p></td>
<td align="left"><p>変換中にハードウェアをクリップできます。</p></td>
</tr>
</tbody>
</table>

 

ハードウェアジオメトリアクセラレータの機能セットは異なる場合があるため (サポートされている光源の数など)、キャップ構造体は、このデバイスが実行するジオメトリ操作のサブセットを示します。 ゼロはサポートされている光源の数の有効な値であり、ハードウェアが変換のみを行うことを示します。

頂点法線を含む頂点のみが適切に点灯します。法線を含まない頂点の場合は、すべての光源の計算に0のドット積が使用されます。

ジオメトリパイプラインのソフトウェア実装で使用されるすべてのキー状態とデータ構造は、DDI レベルで利用可能になります。 一部のディスプレイカードでは、ハードウェアに光を実装するだけで、ホストプロセッサ上での変換とクリッピングが行われます。

次のレンダリング状態の種類は、変換と照明を高速化するデバイスにのみ適用されます。

```cpp
D3DRENDERSTATE_AMBIENT
D3DRENDERSTATE_AMBIENTMATERIALSOURCE
D3DRENDERSTATE_CLIPPING
D3DRENDERSTATE_CLIPPLANEENABLE
D3DRENDERSTATE_COLORVERTEX
D3DRENDERSTATE_DIFFUSEMATERIALSOURCE
D3DRENDERSTATE_EMISSIVEMATERIALSOURCE
D3DRENDERSTATE_EXTENTS
D3DRENDERSTATE_FOGVERTEXMODE
D3DRENDERSTATE_LIGHTING
D3DRENDERSTATE_LOCALVIEWER
D3DRENDERSTATE_NORMALIZENORMALS
D3DRENDERSTATE_SPECULARMATERIALSOURCE
D3DRENDERSTATE_VERTEXBLEND
```

 

 





