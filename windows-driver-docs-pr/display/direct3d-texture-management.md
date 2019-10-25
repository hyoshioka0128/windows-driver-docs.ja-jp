---
title: Direct3D テクスチャの管理
description: Direct3D テクスチャの管理
ms.assetid: d67ce56b-ed76-413f-b09f-e25400f1ac6d
keywords:
- テクスチャ管理 WDK Direct3D
- Direct3D WDK Windows 2000 ディスプレイ、テクスチャ管理
- テクスチャ管理 WDK Direct3D、テクスチャ管理について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b4f4e8477ed1588a0e5079def31671c578beb4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839740"
---
# <a name="direct3d-texture-management"></a>Direct3D テクスチャの管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


テクスチャのサポートは省略可能ですが、今日のドライバーのほとんどは、それをサポートすることができます。 テクスチャマッピングをサポートするドライバーは、Microsoft Direct3D DDI のすべてのテクスチャ関連操作コードに応答する必要があります。 テクスチャ関連の操作コードの詳細については、「 [**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)」を参照してください。

また、ドライバーは、 [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)コールバックを使用して、テクスチャステージの状態を検証する必要があります。

次のセクションでは、ドライバーがテクスチャのサポートを実装する方法について説明します。

[複数のテクスチャ](multiple-textures.md)

[パレット化テクスチャ](paletted-textures.md)

[テクスチャ Blitting](texture-blitting.md)

[ドライバーによって管理されるテクスチャ](driver-managed-textures.md)

[ドライバーによって管理されるリソース](driver-managed-resources.md)

 

 





