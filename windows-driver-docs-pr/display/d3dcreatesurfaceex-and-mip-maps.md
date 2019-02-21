---
title: D3dCreateSurfaceEx と MIP マップ
description: D3dCreateSurfaceEx と MIP マップ
ms.assetid: d0f4ee41-7622-4153-877c-17c88f8147a9
keywords:
- MIP マップ サーフェス WDK Direct3D
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19c652e50ee642e61c4e9c76ed804b7761004be6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552998"
---
# <a name="d3dcreatesurfaceex-and-mip-maps"></a>D3dCreateSurfaceEx と MIP マップ


## <span id="ddk_d3dcreatesurfaceex_and_mip_maps_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_MIP_MAPS_GG"></span>


MIP マップ内の各レベルは、別のハンドル値に関連付けられます。 これらのハンドルがあります、連続するただし。 Direct3D DDI は最上位レベルのサーフェスのハンドルのみが引数として渡されるように設計されています、 **IDirect3DDevice7::SetTexture** (Direct3D SDK のドキュメントで説明)、API のメソッドと、現在詳細のレベルテクスチャの段階の状態で指定された (D3DTSS\_MAXMIPLEVEL)。 MIP マップを使用する最も自然な方法では、MIP マップ全体を表す 1 つのドライバー側構造をビルドします。

 

 





