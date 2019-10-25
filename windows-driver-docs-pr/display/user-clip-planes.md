---
title: ユーザー クリップ平面
description: ユーザー クリップ平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- クリッププレーン WDK Direct3D
- ユーザー定義のクリッププレーン WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f450d693ee1859abe8a6bb56cf3616335aa1c337
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825419"
---
# <a name="user-clip-planes"></a>ユーザー クリップ平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


最新の DirectX リリースでは、ユーザー定義のクリッププレーンが有効になっています。 これらは他のクリッププレーンと同じように動作しますが、アプリケーションで設定できます。 ドライバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)の D3DDP2OP\_SETCLIPPLANE 操作コードに応答することによって、これらのプレーンを処理する必要があります。

 

 





