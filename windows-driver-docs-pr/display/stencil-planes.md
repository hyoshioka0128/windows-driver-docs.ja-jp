---
title: ステンシル平面
description: ステンシル平面
ms.assetid: a2abe78b-7755-45fc-ba02-f2809db5da3e
keywords:
- Direct3D WDK Windows 2000 display、ステンシル平面
- ステンシル平面 WDK Direct3D
- ピクセルごとの描画 (WDK Direct3D)
- 特殊効果 (WDK Direct3D)
- ジオメトリレンダリング WDK Direct3D
- WDK Direct3D の概要
- WDK Direct3D のシャドウ
- decals WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b415fb75187e1ce8ccfdbc49f543d38ba3ca4fb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829440"
---
# <a name="stencil-planes"></a>ステンシル平面


## <span id="ddk_stencil_planes_gg"></span><span id="DDK_STENCIL_PLANES_GG"></span>


ステンシル平面は、ピクセル単位で描画を有効または無効にします。 通常、これらは、decals、アウトライン、影、構築されたソリッドジオメトリレンダリングなどの特殊効果を実現するために、マルチパスアルゴリズムで使用されます。

Direct3D を高速化するために設計された一部のハードウェアは、ステンシル平面を実装します。 ステンシル平面によって実現される特殊効果は、エンターテインメントアプリケーションに役立ちます。

ステンシル平面は、z バッファーデータに埋め込まれると想定されます。

DirectX 5.0 では、アプリケーションは、 [**D3DDEVICEDESC\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)構造体の**Dwdevicezbufferbitdepth**メンバーに設定されている Ddbd\_*Xx*フラグを使用して、使用可能な z バッファーのビット深度を見つけました。 既存の DDBD\_*Xx*フラグを使用して表すことができないステンシルおよび z バッファーのビット深度を持つ z バッファーをサポートするために、DirectX 6.0 以降のバージョンには、新しい API エントリポイント**IDirect3D7:: EnumZBufferFormats**があります (「」を参照)。使用可能な z バッファー/ステンシルのピクセル形式を記述する DDPIXEL 形式の構造体の配列を返す Direct3D SDK ドキュメント)。 [**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の構造体には、次の新しい z バッファー関連のメンバーが含まれています。

<span id="dwStencilBitDepth"></span><span id="dwstencilbitdepth"></span><span id="DWSTENCILBITDEPTH"></span>**dwStencilBitDepth**  
(DDBD\_*Xx*フラグ値ではなく) ステンシルビットの数を整数として指定します。

<span id="dwZBitMask"></span><span id="dwzbitmask"></span><span id="DWZBITMASK"></span>**dwZBitMask マスク**  
Z 値がどのビットを使用するかを指定します。 0以外の場合、このマスクは、z バッファーが標準の符号なし整数の z バッファー形式であることを意味します。

<span id="dwStencilBitMask"></span><span id="dwstencilbitmask"></span><span id="DWSTENCILBITMASK"></span>**dwStencilBitMask**  
ステンシル値が占めるビットを指定します。

新しいフラグ (DDPF\_STENCILBUFFER) は、z バッファー内にステンシルビットが存在することを示します。 前に存在していた**Dwzbufferbitdepth**メンバーは、ステンシルビットを含む z バッファービットの合計数を示します。

DirectX 6.0 以降のバージョンのドライバーでは、サポートする z 専用の z バッファー形式の**Dwdevicezbufferbitdepth**に適切な ddbd\_*Xx*フラグを設定する必要があります。 ステンシル平面がサポートされておらず、DDBD\_*Xx*フラグが使用可能なすべての z バッファー形式を表すことができる場合は、これらのフラグを設定するだけで十分です。これらのフラグは、 **IDirect3D7:: enumzbufferformats**によって ddピクセル形式に変換されるためです。 それ以外の場合、Direct3D ドライバーは、最初の DWORD が有効な z バッファー DDの形式の構造体の数を示し、その後に次の値を示すバッファーを返すことによって、GUID\_Zピクセル形式の GUID を使用する[**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)クエリに応答する必要があります。DDピクセル形式の構造体自体。

次の表に、ステンシル平面に関連付けられた新しいレンダリング状態を示します。表示状態、レンダリング状態の値に関連付けられている型、および説明が表示されます。 これらのレンダリング状態の詳細については、DirectX SDK のドキュメントを参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レンダリング状態</th>
<th align="left">タスクバーの検索ボックスに</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFUNC</p></td>
<td align="left"><p>D3DCMPFUNC</p></td>
<td align="left"><p>比較関数。 次の式が true の場合、テストは成功します。</p>
<p>(ref & mask)OPERATION (ステンシル & mask)。 <em>ref</em>は参照値、<em>ステンシル</em>はステンシルバッファーの値、 <em>mask</em>は D3DRENDERSTATE_STENCILMASK の値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILREF</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシルテストで使用される参照値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシルテストで使用されるマスク値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DRENDERSTATE_STENCILWRITEMASK</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>ステンシルバッファーに書き込まれるすべての値に適用される書き込みマスク。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DRENDERSTATE_STENCILFAIL</p>
<p>D3DRENDERSTATE_STENCILZFAIL</p>
<p>D3DRENDERSTATE_STENCILPASS</p></td>
<td align="left"><p>D3DSTENCILOP</p></td>
<td align="left"><p>これらの新しいレンダリング状態は、それぞれ、ステンシルテストが失敗した場合、ステンシルテストが成功したが z テストに失敗した場合、およびステンシルと z テストの両方が成功した場合にハードウェアに通知するために定義されます。 これらの新しいレンダリング状態の値は、D3DSTENCILOP 列挙型の列挙子に設定できます。列挙型は、実行する必要のあるステンシル操作を指定します。 D3DSTENCILOP の詳細については、DirectX SDK のドキュメントを参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





