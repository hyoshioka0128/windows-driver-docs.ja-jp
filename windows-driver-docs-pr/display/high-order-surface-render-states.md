---
title: 高順序サーフェイスレンダーの状態
description: 高順序サーフェイスレンダーの状態
ms.assetid: c664e0b8-8b96-4f66-bb9c-b87c5d5e7a05
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 表示、高順序サーフェイス、レンダー状態
- 高順序サーフェス WDK DirectX 8.0、レンダー状態
- レンダー状態 WDK DirectX 8.0
- レンダー状態 WDK DirectX 8.0、高順序サーフェス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16c763c9d2dad1134df88fb604d9429a9563e8b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838897"
---
# <a name="high-order-surface-render-states"></a>高順序サーフェイスレンダーの状態


## <span id="ddk_high_order_surface_render_states_gg"></span><span id="DDK_HIGH_ORDER_SURFACE_RENDER_STATES_GG"></span>


高順序サーフェイスで使用されるレンダリング状態は3つあります。 これらのレンダリング状態について以下に説明します。

### <a name="span-idd3drs_patchedgestylespanspan-idd3drs_patchedgestylespand3drs_patchedgestyle"></a><span id="d3drs_patchedgestyle"></span><span id="D3DRS_PATCHEDGESTYLE"></span>D3DRS\_PATCHEDGESTYLE

このレンダリング状態は、修正プログラムのエッジが不連続テセレーションを使用するか、連続して表示するかを制御するために使用されます。 詳細については、DirectX 8.0 SDK のドキュメントを参照してください。

### <a name="span-idd3drs_patchsegmentsspanspan-idd3drs_patchsegmentsspand3drs_patchsegments"></a><span id="d3drs_patchsegments"></span><span id="D3DRS_PATCHSEGMENTS"></span>D3DRS\_パッチセグメント

このレンダー状態は、パッチの各エッジに使用されるセグメントの数を示します。 DP2 トークンに明示的な数のセグメントが指定されている場合、これらのセグメントはこのレンダリング状態の値をオーバーライドする必要があります。 詳細については、DirectX 8.0 SDK のドキュメントを参照してください。

### <a name="span-idd3drs_deletertpatchspanspan-idd3drs_deletertpatchspan-d3drs_deletertpatch"></a><span id="d3drs_deletertpatch"></span><span id="D3DRS_DELETERTPATCH"></span>D3DRS\_DELETERTPATCH

このレンダー状態は、修正プログラムが削除されることをドライバーに通知します。 詳細については、「 [**D3DRENDERSTATETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3drenderstatetype)」を参照してください。

 

 





