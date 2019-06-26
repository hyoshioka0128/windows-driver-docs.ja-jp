---
title: ステンシル平面
description: ステンシル平面
ms.assetid: a2abe78b-7755-45fc-ba02-f2809db5da3e
keywords:
- Direct3D WDK Windows 2000 の表示、ステンシル平面
- ステンシル平面を WDK Direct3D
- ピクセルあたりの描画の WDK Direct3D
- WDK Direct3D の特殊効果
- ジオメトリの WDK Direct3D のレンダリング
- WDK Direct3D のアウトライン表示
- WDK Direct3D のシャドウ
- デカール WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8697b312d09d160084ae8aa38761c5c5ad1907
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376030"
---
# <a name="stencil-planes"></a>ステンシル平面


## <span id="ddk_stencil_planes_gg"></span><span id="DDK_STENCIL_PLANES_GG"></span>


ステンシル平面は有効にし、ピクセル単位で描画を無効にします。 通常、マルチパスのアルゴリズムでデカール、アウトライン、影、建設的な信頼性の高いジオメトリのレンダリングなどの特殊効果を実現するためには使用されます。

一部のハードウェアは Direct3D 実装ステンシル平面を促進します。 ステンシルの面で有効になって特殊効果は、entertainment アプリケーションに役立ちます。

ステンシル平面は、z バッファーのデータに埋め込まれると見なされます。

DirectX 5.0 では、アプリケーションが、DDBD を使用して利用可能な z バッファー ビット深度\_*Xx*フラグ設定、 **dwDeviceZBufferBitDepth**のメンバー、 [ **D3DDEVICEDESC\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)構造体。 ステンシルと z バッファーで z バッファーをサポートするためにビット深度既存 DDBD で表現できない\_*Xx*フラグ、DirectX 6.0 およびそれ以降のバージョン、新しい API のエントリ ポイントがある**IDirect3D7:。EnumZBufferFormats** (Direct3D SDK のドキュメントで説明)、可能な z バッファー/ステンシル ピクセル形式を記述する DDPIXELFORMAT 構造体の配列が返されます。 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)構造体には、次の新しい z バッファー関連メンバーが含まれています。

<span id="dwStencilBitDepth"></span><span id="dwstencilbitdepth"></span><span id="DWSTENCILBITDEPTH"></span>**dwStencilBitDepth**  
ステンシルのビット数を指定します (、DDBD としてではなく、整数として\_*Xx*フラグ値)。

<span id="dwZBitMask"></span><span id="dwzbitmask"></span><span id="DWZBITMASK"></span>**dwZBitMask**  
Z 値を占有するビットを指定します。 ゼロ以外の場合、このマスクは、z バッファーが、標準化された符号なし整数の z バッファー形式であります。

<span id="dwStencilBitMask"></span><span id="dwstencilbitmask"></span><span id="DWSTENCILBITMASK"></span>**dwStencilBitMask**  
ステンシルの値を占有するビットを指定します。

新しいフラグを DDPF\_STENCILBUFFER、ステンシル ビット z バッファー内の存在を示します。 **DwZBufferBitDepth** 、以前に存在していた場合は、メンバーなど、ステンシル ビット z バッファー ビットの合計数がわかります。

DirectX 6.0 以降のバージョンのドライバーでは、適切な DDBD を設定する必要がありますも\_*Xx*のフラグ**dwDeviceZBufferBitDepth** z のみ z バッファー形式のサポートします。 ステンシルの平面がサポートされていない場合と、DDBD\_*Xx*フラグは、すべての利用可能な z バッファー形式で表すことができます、によって DDPIXELFORMAT に変換されるため、十分ではこれらのフラグを設定し、 **IDirect3D7::EnumZBufferFormats**します。 それ以外の場合、Direct3D ドライバーに応答する必要があります、 [ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) GUID を使用するクエリ\_最初 DWORD がの数を示しますバッファーを返すことによって ZPixelFormats GUIDDDPIXELFORMAT 構造自体で後に、有効な z バッファー DDPIXELFORMAT 構造。

ステンシル平面に関連付けられている描画状態の新しいレンダリング状態、レンダリング状態の値、および説明に関連付けられている型を一覧表示、次の表に表示されます。 詳細については、この状態の表示、DirectX SDK のマニュアルを参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レンダリングの状態</th>
<th align="left">種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFUNC</p></td>
<td align="left"><p>D3DCMPFUNC</p></td>
<td align="left"><p>比較関数。 テストは、次の式が true の場合に渡します。</p>
<p>(ref & マスク)操作 (ステンシル & マスク) を<em>ref</em>参照の値は、<em>ステンシル</em>、ステンシル バッファーの値と<em>マスク</em>D3DRENDERSTATE_STENCILMASK の値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILREF</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシル テストに使用される値を参照します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシル テストに使用される値をマスクします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILWRITEMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシル バッファーに書き込まれたすべての値に適用するマスクを記述します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFAIL</p>
<p>D3DRENDERSTATE_STENCILZFAIL</p>
<p>D3DRENDERSTATE_STENCILPASS</p></td>
<td align="left"><p>D3DSTENCILOP</p></td>
<td align="left"><p>これら新しいレンダリング状態が定義されて、それぞれ、ステンシル テストが失敗した場合の対処方法について、ハードウェアを通知するために、ステンシルと z 検定を渡すときに、ステンシル テストに合格するが、z テストが失敗したときに。 これらの新しいレンダリング状態の値は、実行する目的のステンシルの操作を指定する、D3DSTENCILOP 列挙型の列挙子を設定できます。 D3DSTENCILOP の詳細については、DirectX SDK のドキュメントを参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





