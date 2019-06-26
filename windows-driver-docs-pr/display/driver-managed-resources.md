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
ms.openlocfilehash: 68e935462ea876a3c11ee2bc4b4a747d7bdf1c4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353849"
---
# <a name="driver-managed-resources"></a>ドライバー管理対象リソース


## <span id="ddk_driver_managed_resources_gg"></span><span id="DDK_DRIVER_MANAGED_RESOURCES_GG"></span>


」の説明に従ってテクスチャの管理をサポートしているだけでなく[Driver-Managed テクスチャ](driver-managed-textures.md)、DirectX 8.1 ドライバーもリソースを管理できる一般に、テクスチャ、テクスチャのボリューム、キューブ マップのテクスチャ、頂点バッファー、およびインデックスなどバッファー。

ドライバーを設定してドライバー-マネージ リソースをサポートする、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体を DDCAPS2\_CANMANAGERESOURCE ビット. ドライバーでは、この DDCORECAPS 構造を指定します、 **ddCaps**のメンバー、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体。 DD\_HALINFO がによって返される[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)ドライバーの DirectDraw コンポーネントの初期化に応答します。

 

 





