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
ms.openlocfilehash: 9a65280100a9285f42e5027e2432fa1c69c0b5a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549994"
---
# <a name="direct3d-texture-management"></a>Direct3D テクスチャの管理


## <span id="ddk_direct3d_texture_management_gg"></span><span id="DDK_DIRECT3D_TEXTURE_MANAGEMENT_GG"></span>


テクスチャのサポートはオプションですが、今日のドライバーの大部分はそれをサポートできます。 テクスチャのマッピングをサポートするドライバーは、すべてのテクスチャに関連する操作コードでは、マイクロソフトの Direct3D DDI に応答する必要があります。 テクスチャに関連する操作のコードの詳細については、次を参照してください。 [ **D3DHAL\_DP2OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff545678)します。

ドライバーもでテクスチャ ステージの状態を検証する必要があります、 [ **D3dValidateTextureStageState** ](https://msdn.microsoft.com/library/windows/hardware/ff549064)コールバック。

次のセクションでは、ドライバーがテクスチャのサポートを実装する方法について説明します。

[複数のテクスチャ](multiple-textures.md)

[パレット化されたテクスチャ](paletted-textures.md)

[テクスチャ中](texture-blitting.md)

[ドライバー管理のテクスチャ](driver-managed-textures.md)

[ドライバー管理リソース](driver-managed-resources.md)

 

 





