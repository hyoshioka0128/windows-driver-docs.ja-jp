---
title: 高注文画面描画状態
description: 高注文画面描画状態
ms.assetid: c664e0b8-8b96-4f66-bb9c-b87c5d5e7a05
keywords:
- DirectX 8.0 リリース ノート WDK Windows 2000 の表示、上位のサーフェスの状態を表示します。
- 上位のサーフェス WDK DirectX 8.0 では、状態を表示します。
- WDK DirectX 8.0 の状態を表示します。
- WDK DirectX 8.0 では、上位のサーフェスの状態を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df0e494a2d1bfd1071c9632aca13f96027da877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560945"
---
# <a name="high-order-surface-render-states"></a>高注文画面描画状態


## <span id="ddk_high_order_surface_render_states_gg"></span><span id="DDK_HIGH_ORDER_SURFACE_RENDER_STATES_GG"></span>


上位サーフェスで使用される 3 つの描画状態があります。 これらのレンダリングの状態は次のとおりです。

### <a name="span-idd3drspatchedgestylespanspan-idd3drspatchedgestylespand3drspatchedgestyle"></a><span id="d3drs_patchedgestyle"></span><span id="D3DRS_PATCHEDGESTYLE"></span>D3DRS\_PATCHEDGESTYLE

このレンダリング状態は、修正プログラムのエッジが不連続または連続のテセレーションを使用するかどうかを制御するために使用されます。 詳細については、DirectX 8.0 SDK ドキュメントを参照してください。

### <a name="span-idd3drspatchsegmentsspanspan-idd3drspatchsegmentsspand3drspatchsegments"></a><span id="d3drs_patchsegments"></span><span id="D3DRS_PATCHSEGMENTS"></span>D3DRS\_PATCHSEGMENTS

これは、修正プログラムの各辺に使用するセグメントの数を状態によりにレンダリングします。 これらのセグメントは、この値をオーバーライドする必要があります DP2 トークンで、明示的なセグメント数が指定されている場合は、状態を表示します。 詳細については、DirectX 8.0 SDK ドキュメントを参照してください。

### <a name="span-idd3drsdeletertpatchspanspan-idd3drsdeletertpatchspan-d3drsdeletertpatch"></a><span id="d3drs_deletertpatch"></span><span id="D3DRS_DELETERTPATCH"></span> D3DRS\_DELETERTPATCH

このレンダリング状態では、修正プログラムが削除するのには、ドライバーに通知します。 詳細については、[ **D3DRENDERSTATETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff549036)を参照してください。

 

 





