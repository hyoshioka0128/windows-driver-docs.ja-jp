---
title: 動的な頂点バッファーとインデックス バッファー
description: 動的な頂点バッファーとインデックス バッファー
ms.assetid: 81ee22c6-3f98-4767-a4cd-a7907ed8f8a2
keywords:
- 動的頂点 WDK DirectX 9.0
- インデックス バッファー WDK DirectX 9.0
- 動的なバッファー WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05fcfc74dbc1b47759e7881d81457553fc2fc53f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383097"
---
# <a name="dynamic-vertex-and-index-buffers"></a>動的な頂点バッファーとインデックス バッファー


## <span id="ddk_dynamic_vertex_and_index_buffers_gg"></span><span id="DDK_DYNAMIC_VERTEX_AND_INDEX_BUFFERS_GG"></span>


動的頂点またはインデックス バッファーは、頻繁にアプリケーションのロックと書き込みをリソースです。 ドライバーの呼び出しでの動的なバッファーのロック時[ *LockD3DBuffer* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))関数の場合、DDLOCK\_OKTOSWAP ビット (D3DLOCK とも呼ばれます\_破棄ビット)、の**dwFlags** 、DD のメンバー\_呼び出し元が、バッファーの既存の内容を必要としないことを示す LOCKDATA 構造を設定することができます。 そのため、ドライバーは、データをバッファーするポインターを返す前に、内容を破棄できます。 呼び出し元に、既存の内容を必要としないため、ドライバーの名前を変更バッファー設定、 **fpVidMem** 、DD のメンバー\_画面\_バッファーに新しい値のグローバル構造体。 バッファー (つまり、複数のバッファリングを設定) の名前を変更するには、ドライバーは、ハードウェアの停止を回避します。

DDLOCK\_OKTOSWAP ビットは、動的なバッファーをロックして静的バッファーをロックすることはありませんのみ設定できます。

ドライバーが動的でバッファーのサイズを格納する必要がありますに注意してください[AGP](agp-support.md)メモリ バスのパフォーマンスを真剣に可能性がある場合、動的バッファーのサイズはローカルのビデオ メモリに格納され、アプリケーションでは、これらのバッファーにデータを書き込みます連番でない方法で、ため。影響を受けます。

 

 





