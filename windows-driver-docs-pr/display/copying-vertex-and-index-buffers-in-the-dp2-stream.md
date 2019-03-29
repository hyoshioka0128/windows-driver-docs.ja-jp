---
title: DP2 ストリームでの頂点バッファーとインデックス バッファーのコピー
description: DP2 ストリームでの頂点バッファーとインデックス バッファーのコピー
ms.assetid: 5181e299-4beb-448c-bf11-be9bb5575af1
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示 DP2 描画トークン
- DP2 描画トークン WDK DirectX 8.0
- 描画トークン WDK DirectX 8.0
- トークンの WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 825138c82c713f1f8b661aa7bb77513a0e15642e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578163"
---
# <a name="copying-vertex-and-index-buffers-in-the-dp2-stream"></a>DP2 ストリームでの頂点バッファーとインデックス バッファーのコピー


## <span id="ddk_copying_vertex_and_index_buffers_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VERTEX_AND_INDEX_BUFFERS_IN_THE_DP2_STREAM_GG"></span>


新しい DP2 トークン、D3DDP2OP\_BUFFERBLT が最適なコピーとインデックスと頂点バッファーの更新をサポートするために追加されました。 このトークンは、既存の D3DDP2OP によく似ています\_TEXBLT コピーしテクスチャの更新だけが、単純な四角形ではなくコピー subbuffer をサポートするために変更されたをします。

 

 





