---
title: 複数レンダー ターゲットおよび深度ステンシルの設定
description: 複数レンダー ターゲットおよび深度ステンシルの設定
ms.assetid: 98acd448-0b65-4a3a-9e95-8e753729a7d7
keywords:
- レンダーターゲット WDK DirectX 9.0、複数
- 複数のレンダーターゲット WDK DirectX 9.0
- 深度ステンシル WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d50c7aeddb97ce5a3ea3ca4d293592e658604db2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825813"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>複数レンダー ターゲットおよび深度ステンシルの設定


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 バージョンのドライバーでは、[複数のターゲットへの同時レンダリング](rendering-to-multiple-targets-simultaneously.md)がサポートされていない場合でも、 [**D3DDRAWPRIMITIVES2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数で D3DDP2OP\_SETRENDERTARGET2 および D3DDP2OP\_SETDEPTHSTENCIL 操作コードを処理する必要があります。 [**D3DHAL\_DP2SETRENDERTARGET2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2)と[**D3DHAL\_DP2SETDEPTHSTENCIL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil)構造体はそれぞれ、[コマンドストリーム](command-stream.md)で次のコードに従います。

 

 





