---
title: Direct3D コンテキストに関連付けられたオブジェクトの破棄
description: Direct3D コンテキストに関連付けられたオブジェクトの破棄
ms.assetid: b464eb31-6062-4c0c-90a2-2de39b5a85ac
keywords:
- WDK DirectX 9.0 のメモリ リークします。
- コンテキスト WDK Direct3D、DirectX 9.0
- WDK DirectX 9.0 のコンテキストに関連付けられたオブジェクトの破棄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361bf31541addd0034a9d46e6e016bd544d16cb3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384886"
---
# <a name="destroying-objects-associated-with-a-direct3d-context"></a>Direct3D コンテキストに関連付けられたオブジェクトの破棄


## <span id="ddk_destroying_objects_associated_with_a_direct3d_context_gg"></span><span id="DDK_DESTROYING_OBJECTS_ASSOCIATED_WITH_A_DIRECT3D_CONTEXT_GG"></span>


このトピックには、DirectX 7.0 以降が適用されます。

ように、メモリ リーク、ディスプレイ ドライバーは、Direct3D のコンテキストに関連付けられたすべてのオブジェクトを解放する必要がありますと、ドライバーの[ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)関数が呼び出されます。 これらのオブジェクトが含まれて、たとえば、頂点とピクセル[シェーダー](direct3d-shaders.md)、[宣言と頂点シェーダーのコード](separating-declarations-and-code-for-vertex-shaders.md)、リソースの[非同期クエリ](supporting-asynchronous-query-operations.md)、およびテクスチャリソース。

 

 





