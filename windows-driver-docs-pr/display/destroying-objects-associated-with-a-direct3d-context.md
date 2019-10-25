---
title: Direct3D コンテキストに関連付けられているオブジェクトの破棄
description: Direct3D コンテキストに関連付けられているオブジェクトの破棄
ms.assetid: b464eb31-6062-4c0c-90a2-2de39b5a85ac
keywords:
- メモリリーク WDK DirectX 9.0
- コンテキスト WDK Direct3D、DirectX 9.0
- コンテキスト WDK DirectX 9.0 に関連付けられているオブジェクトの破棄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee365eaab274ff4ba925971823e57c14b6be57bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839755"
---
# <a name="destroying-objects-associated-with-a-direct3d-context"></a>Direct3D コンテキストに関連付けられているオブジェクトの破棄


## <span id="ddk_destroying_objects_associated_with_a_direct3d_context_gg"></span><span id="DDK_DESTROYING_OBJECTS_ASSOCIATED_WITH_A_DIRECT3D_CONTEXT_GG"></span>


このトピックは、DirectX 7.0 以降に適用されます。

メモリリークを防ぐために、ドライバーの[**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)関数が呼び出されたときに、ディスプレイドライバーが Direct3D コンテキストに関連付けられているすべてのオブジェクトを解放する必要があります。 これらのオブジェクトには、たとえば、頂点[シェーダー](direct3d-shaders.md)、[頂点シェーダーの宣言とコード](separating-declarations-and-code-for-vertex-shaders.md)、[非同期クエリ](supporting-asynchronous-query-operations.md)用のリソース、テクスチャリソースなどがあります。

 

 





