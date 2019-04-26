---
title: ストリームでオフセットを共有する頂点要素のサポート
description: ストリームでオフセットを共有する頂点要素のサポート
ms.assetid: 52b2d891-15a1-4b82-aaf2-634f33202974
keywords:
- 頂点シェーダー宣言 WDK DirectX 9.0、ストリーム内のオフセットの共有
- シェーダー宣言 WDK DirectX 9.0、ストリーム内のオフセットの共有
- 頂点のストリームのオフセット WDK DirectX 9.0
- 頂点のストリームのオフセット WDK DirectX 9.0、頂点シェーダーの宣言
- ストリームのオフセット WDK DirectX 9.0
- ストリームのオフセット WDK DirectX 9.0、頂点シェーダーの宣言
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbe198f9fda0496b165a28b90df11fb4499feee9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350106"
---
# <a name="supporting-vertex-elements-sharing-offset-in-a-stream"></a>ストリームでオフセットを共有する頂点要素のサポート


## <span id="ddk_supporting_vertex_elements_sharing_offset_in_a_stream_gg"></span><span id="DDK_SUPPORTING_VERTEX_ELEMENTS_SHARING_OFFSET_IN_A_STREAM_GG"></span>


DirectX 9.0 バージョンのドライバーでは、そのデバイスが、D3DDEVCAPS2 を設定して、ストリーム内の同一オフセットを共有する複数の頂点要素を使用することを示します\_VERTEXELEMENTSCANSHARESTREAMOFFSET 機能ビット、 **DevCaps2**D3DCAPS9 構造体のメンバーです。 頂点シェーダーの宣言は、頂点の要素の配列で構成されます。 詳細については、次を参照してください。[宣言の分離と頂点シェーダーのコード](separating-declarations-and-code-for-vertex-shaders.md)します。

ピクセル シェーダー (PS) バージョン 3.0 以前をサポートしているデバイスの DirectX 9.0 ドライバー設定 D3DDEVCAPS2 場合\_VERTEXELEMENTSCANSHARESTREAMOFFSET、ドライバーが処理できる、D3DDECLUSAGE を指定する要素を持つほとんどの頂点宣言\_POSITIONT (0) の使用法の種類。 D3DDECLUSAGE でこの事前 PS 3.0 ドライバーに変換します頂点宣言\_POSITIONT (0) に柔軟な頂点の有効な形式 (FVF)。 ただし、この事前 PS 3.0 のドライバーが、D3DDECLUSAGE を指定する要素を持つ頂点宣言を処理できない\_POSITIONT (0) の使用法の種類宣言では、テクスチャ座標のギャップがある場合。 たとえば、この事前 PS 3.0 のドライバーでは、頂点の次の宣言を処理できません。

```cpp
{0,0,D3DDECLTYPE_FLOAT4, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_POSITIONT, 0}
{0,16,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 0}
{0,24,D3DDECLTYPE_FLOAT2, D3DDECLMETHOD_DEFAULT, D3DDECLUSAGE_TEXCOORD, 5}
```

テクスチャ座標のギャップがあるため、この事前 PS 3.0 のドライバーが、D3DDECLUSAGE を表現できない\_FVF を使用して、テクスチャ座標の要素。

ピクセル シェーダー 3.0 以降をサポートするデバイス用の DirectX 9.0 ドライバー設定 D3DDEVCAPS2 場合\_VERTEXELEMENTSCANSHARESTREAMOFFSET、ドライバーは、D3DDECLUSAGE を指定する要素を持つすべての頂点宣言を処理する必要があります\_POSITIONT (0) の使用法の種類。 このドライバーは、複数の頂点の要素をさせる必要があります。

-   ストリーム内の同一オフセットを共有します。

-   さまざまな種類があります。 そのため、さまざまなサイズがあることができます。

-   任意に重複します。 たとえば、別の要素の途中であるストリームの位置にある 1 つの要素を開始できます。

 

 





