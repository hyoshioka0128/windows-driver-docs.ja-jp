---
title: ドライバー管理対象リソース
description: ドライバー管理対象リソース
ms.assetid: f68b622a-247a-4a89-8d4c-c6a306b7fb3e
keywords:
- テクスチャ WDK Direct3D、ドライバーで管理されたリソースの管理
- WDK Direct3D ドライバー管理リソース
- 管理しやすいリソース WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1c121318728f1aeddec194d24fbd503471be60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391507"
---
# <a name="driver-managed-resources"></a>ドライバー管理対象リソース


## <span id="ddk_driver_managed_resources_gg"></span><span id="DDK_DRIVER_MANAGED_RESOURCES_GG"></span>


」の説明に従ってテクスチャの管理をサポートしているだけでなく[Driver-Managed テクスチャ](driver-managed-textures.md)、DirectX 8.1 ドライバーもリソースを管理できる一般に、テクスチャ、テクスチャのボリューム、キューブ マップのテクスチャ、頂点バッファー、およびインデックスなどバッファー。

ドライバーを設定してドライバー-マネージ リソースをサポートする、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造体を DDCAPS2\_CANMANAGERESOURCE ビット. ドライバーでは、この DDCORECAPS 構造を指定します、 **ddCaps**のメンバー、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体。 DD\_HALINFO がによって返される[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)ドライバーの DirectDraw コンポーネントの初期化に応答します。

 

 





