---
title: Direct3D テクスチャの管理
description: Direct3D テクスチャの管理
ms.assetid: d67ce56b-ed76-413f-b09f-e25400f1ac6d
keywords:
- WDK Direct3D テクスチャの管理
- Direct3D WDK Windows 2000 の表示、テクスチャの管理
- テクスチャ管理 WDK の Direct3D テクスチャの管理について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ede23899b81c0d4120fd564a3d24c52e64d62dc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384861"
---
# <a name="direct3d-texture-management"></a>Direct3D テクスチャの管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


テクスチャのサポートはオプションですが、今日のドライバーの大部分はそれをサポートできます。 テクスチャのマッピングをサポートするドライバーは、すべてのテクスチャに関連する操作コードでは、マイクロソフトの Direct3D DDI に応答する必要があります。 テクスチャに関連する操作のコードの詳細については、次を参照してください。 [ **D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)します。

ドライバーもでテクスチャ ステージの状態を検証する必要があります、 [ **D3dValidateTextureStageState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)コールバック。

次のセクションでは、ドライバーがテクスチャのサポートを実装する方法について説明します。

[複数のテクスチャ](multiple-textures.md)

[パレット化されたテクスチャ](paletted-textures.md)

[テクスチャ中](texture-blitting.md)

[ドライバー管理のテクスチャ](driver-managed-textures.md)

[ドライバー管理リソース](driver-managed-resources.md)

 

 





