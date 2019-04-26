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
ms.openlocfilehash: aaa2d306fd89244ff0ca702ab85039f63c100b1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348851"
---
# <a name="destroying-objects-associated-with-a-direct3d-context"></a>Direct3D コンテキストに関連付けられたオブジェクトの破棄


## <span id="ddk_destroying_objects_associated_with_a_direct3d_context_gg"></span><span id="DDK_DESTROYING_OBJECTS_ASSOCIATED_WITH_A_DIRECT3D_CONTEXT_GG"></span>


このトピックには、DirectX 7.0 以降が適用されます。

ように、メモリ リーク、ディスプレイ ドライバーは、Direct3D のコンテキストに関連付けられたすべてのオブジェクトを解放する必要がありますと、ドライバーの[ **D3dContextDestroy** ](https://msdn.microsoft.com/library/windows/hardware/ff542180)関数が呼び出されます。 これらのオブジェクトが含まれて、たとえば、頂点とピクセル[シェーダー](direct3d-shaders.md)、[宣言と頂点シェーダーのコード](separating-declarations-and-code-for-vertex-shaders.md)、リソースの[非同期クエリ](supporting-asynchronous-query-operations.md)、およびテクスチャリソース。

 

 





