---
title: ユーザー クリップ平面
description: ユーザー クリップ平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- クリップ面 WDK Direct3D
- ユーザー定義のクリップ平面を WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc27498278c10ddee4d32d1930caf5421fc6b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389755"
---
# <a name="user-clip-planes"></a>ユーザー クリップ平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


最新の平面が有効になっているユーザー定義のクリップ DirectX を解放します。 これらの作業と同様に他のクリップの面が、アプリケーションで設定可能です。 ドライバーは、D3DDP2OP に応答してこれらの平面を処理する必要があります\_SETCLIPPLANE 操作のコードで[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)します。

 

 





