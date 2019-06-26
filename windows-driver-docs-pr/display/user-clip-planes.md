---
title: ユーザー クリップ平面
description: ユーザー クリップ平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- クリップ面 WDK Direct3D
- ユーザー定義のクリップ平面を WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef90b1ca0ee195d96df5b8cf3268a165cd43673d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373614"
---
# <a name="user-clip-planes"></a>ユーザー クリップ平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


最新の平面が有効になっているユーザー定義のクリップ DirectX を解放します。 これらの作業と同様に他のクリップの面が、アプリケーションで設定可能です。 ドライバーは、D3DDP2OP に応答してこれらの平面を処理する必要があります\_SETCLIPPLANE 操作のコードで[ **D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)します。

 

 





