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
ms.openlocfilehash: c40ad3691dc2d992b14c7bd064a33fe9c66b4e7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365565"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>複数レンダー ターゲットおよび深度ステンシルの設定


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 バージョンのドライバーが D3DDP2OP を処理する必要があります\_SETRENDERTARGET2 と D3DDP2OP\_SETDEPTHSTENCIL 操作のコードでその[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の場合でも、サポートしていません[同時に複数のターゲットにレンダリング](rendering-to-multiple-targets-simultaneously.md)します。 [**D3DHAL\_DP2SETRENDERTARGET2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2)と[ **D3DHAL\_DP2SETDEPTHSTENCIL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil)構造体は、これらのコードで、それぞれに従ってください。[コマンド ストリーム](command-stream.md)します。

 

 





