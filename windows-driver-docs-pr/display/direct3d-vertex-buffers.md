---
title: Direct3D 頂点バッファー
description: Direct3D 頂点バッファー
ms.assetid: b93278fc-c05f-40d4-aec1-7a90aed18ff4
keywords:
- 頂点バッファー WDK Direct3D
- WDK Direct3D のバッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1234f945db3917e4ae9a48467aed41c0ec5297a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839004"
---
# <a name="direct3d-vertex-buffers"></a>Direct3D 頂点バッファー


## <span id="ddk_direct3d_vertex_buffers_gg"></span><span id="DDK_DIRECT3D_VERTEX_BUFFERS_GG"></span>


頂点バッファーには、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)を呼び出すと、コマンドバッファーのプリミティブに関連付けられている頂点データが格納されます。 頂点は、フレキシブル頂点形式 ([FVF](fvf--flexible-vertex-format-.md)) を使用して表されます。各頂点には、次のデータを関連付けることができます。

-   位置 (*x、y、z、および省略可能な w*) (必須)

-   拡散色 (オプション)

-   反射色 (オプション)

-   テクスチャ座標 (省略可能)。 Direct3D は、最大8セット (*u, v*) の値を送信できます。

ドライバーは FVF サポートを提供する必要があります。

実際の頂点と処理される順序は、コマンドバッファーから解析したばかりの D3DDP2OP\_*Xxx*プリミティブコマンドによって異なります。 詳細については、個々の D3DHAL\_DP2*Xxx*の構造リファレンスページを参照してください。

 

 





