---
title: 複数レンダー ターゲットおよび深度ステンシルの設定
description: 複数レンダー ターゲットおよび深度ステンシルの設定
ms.assetid: 98acd448-0b65-4a3a-9e95-8e753729a7d7
keywords:
- レンダー ターゲットの WDK DirectX 9.0 では、複数
- 複数のレンダー ターゲット WDK DirectX 9.0
- 深度ステンシル WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0b65a37d0bf0134105190c7a20925230b3527a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390447"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>複数レンダー ターゲットおよび深度ステンシルの設定


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 バージョンのドライバーが D3DDP2OP を処理する必要があります\_SETRENDERTARGET2 と D3DDP2OP\_SETDEPTHSTENCIL 操作のコードでその[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)関数の場合でも、サポートしていません[同時に複数のターゲットにレンダリング](rendering-to-multiple-targets-simultaneously.md)します。 [**D3DHAL\_DP2SETRENDERTARGET2** ](https://msdn.microsoft.com/library/windows/hardware/ff545785)と[ **D3DHAL\_DP2SETDEPTHSTENCIL** ](https://msdn.microsoft.com/library/windows/hardware/ff545724)構造体は、これらのコードで、それぞれに従ってください。[コマンド ストリーム](command-stream.md)します。

 

 





