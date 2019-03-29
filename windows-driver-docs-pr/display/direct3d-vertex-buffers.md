---
title: Direct3D 頂点バッファー
description: Direct3D 頂点バッファー
ms.assetid: b93278fc-c05f-40d4-aec1-7a90aed18ff4
keywords:
- 頂点バッファー WDK Direct3D
- WDK Direct3D バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2d924a3bfcafabe0c15f9294a814012af08d8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581027"
---
# <a name="direct3d-vertex-buffers"></a>Direct3D 頂点バッファー


## <span id="ddk_direct3d_vertex_buffers_gg"></span><span id="DDK_DIRECT3D_VERTEX_BUFFERS_GG"></span>


頂点バッファーへの呼び出しで、コマンド バッファーのプリミティブに関連付けられている頂点データを格納して[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)します。 頂点は、柔軟な頂点の形式を使用して表されます ([FVF](fvf--flexible-vertex-format-.md))、各頂点が関連付けられている次のデータがあることができます。

-   位置 (*x、y、z、および省略可能な w*) (必須)

-   (省略可能) の拡散色

-   反射色 (省略可能)

-   テクスチャ座標は (省略可能)。 Direct3D はの 8 つのセットの最大値送信できます (*u, v*) 値。

ドライバーは、FVF サポートを提供する必要があります。

実際の頂点と処理する順序は、D3DDP2OP に依存\_*Xxx*プリミティブのコマンドをコマンド バッファーから解析しました。 詳細については、個々 の D3DHAL を参照してください。\_DP2*Xxx*リファレンス ページを構造体。

 

 





