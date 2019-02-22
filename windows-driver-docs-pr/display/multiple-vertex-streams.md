---
title: 複数の頂点のストリーム
description: 複数の頂点のストリーム
ms.assetid: aaaea27b-79e0-4c48-9102-898b42a1487f
keywords:
- WDK の Windows 2000 の表示、複数のストリームの頂点の DirectX 8.0 リリース ノートします。
- 複数の頂点 WDK DirectX 8.0 をストリームします。
- 頂点 WDK DirectX 8.0 の複数のストリーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd942a1d9b9f154807319484fdd6f5bd16fdc3e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561140"
---
# <a name="multiple-vertex-streams"></a>複数の頂点のストリーム


## <span id="ddk_multiple_vertex_streams_gg"></span><span id="DDK_MULTIPLE_VERTEX_STREAMS_GG"></span>


DirectX 8.0 では、複数の頂点のストリームのサポートを追加します。 ドライバーが、DP2 トークンのバインド ストリームを処理する必要がありますも、ドライバーとハードウェアの組み合わせが頂点データの 1 つ以上のストリームをサポートしていない場合でも (D3DDP2OP\_SETSTREAMSOURCE と D3DDP2OP\_SETSTREAMSOURCEUM) と、新しい頂点のストリーム ベースの DP2 描画トークン (を参照してください[新しい DP2 Stream 描画トークン](new-dp2-stream-drawing-tokens.md))。 これらは、描画の DirectX 8.0 ドライバーのドライバーに頂点データを渡すためのメカニズムです。

 

 





