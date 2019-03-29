---
title: ハードウェアの変換とライティング
description: ハードウェアの変換とライティング
ms.assetid: b45aa56e-2d8c-412a-b581-a1e2002d4fac
keywords:
- ハードウェア tansform および照明は、Direct3D WDK Windows 2000 の表示
- WDK Direct3D テクスチャの変換
- WDK Direct3D を変換します。
- 照明 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916c16e09399ab24b96666131ac5fc9cb32e9cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574960"
---
# <a name="hardware-transform-and-lighting"></a>ハードウェアの変換とライティング


## <span id="ddk_hardware_transform_and_lighting_gg"></span><span id="DDK_HARDWARE_TRANSFORM_AND_LIGHTING_GG"></span>


変更せずに照明や変換など、geometry 操作のハードウェア アクセラレータが有効になって、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI 直接 X の最新のリリース。 API レベルでは、ハードウェアで頂点の操作をサポートするデバイスがからラスタライズのみを個別に列挙されます。

既存の caps 構造体は、ハードウェア アクセラレータを使用した変換のデバイス上に存在する可能性のある機能を示すために拡張されています。 サポートされている光源の数を設定するなど、 **dwNumLights**のメンバー、 [ **D3DLIGHTINGCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff548471) と共に報告されます構造[ **D3DDEVICEDESC\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff544689)構造体。

その他のフラグは、次の表のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_CANBLTSYSTONONLOCAL</p></td>
<td align="left"><p>デバイスでテクスチャをサポートする非ローカルのビデオ メモリをシステム メモリから blt します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_DRAWPRIMITIVES2EX</p></td>
<td align="left"><p>ドライバーは、拡張をサポートすることによって 7.0 互換の DirectX が<em>D3dDrawPrimitives2</em>機能します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_HWRASTERIZATION</p></td>
<td align="left"><p>デバイスでは、ラスタライズのハードウェア アクセラレータがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDEVCAPS_HWTRANSFORMANDLIGHT</p></td>
<td align="left"><p>デバイスがハードウェアでは、ハードウェア変換および照明は、両方をサポートできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDEVCAPS_SEPARATETEXTUREMEMORIES</p></td>
<td align="left"><p>デバイスが別のメモリ プールからテクスチャ リングします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTRANSFORMCAPS_CLIP</p></td>
<td align="left"><p>変換中には、ハードウェアがクリップことができます。</p></td>
</tr>
</tbody>
</table>

 

機能が設定されるため (光源がサポートされている数) などのハードウェアのジオメトリのアクセラレータが異なる場合があります、caps 構造体を示すジオメトリ操作のうち、どのサブセットこのデバイスを実行します。 0 は、光源、サポートされている、ハードウェアでは変換のみを示す数の有効な値です。

頂点の法線が含まれる頂点のみは正しく点灯しています。法線が含まれていない頂点、0 のドット積はすべての照明計算に使用します。

すべてのキーの状態とデータ構造体ジオメトリのパイプラインのソフトウェアの実装で使用される DDI レベルでは利用できます。 のみ、いくつか表示カードは、ハードウェアの照明を実装して、変形とクリッピング ホスト プロセッサ上の操作を行います。

次に、型に変換および照明は、高速化するデバイスのみに関連する状態を表示します。

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

 

 





