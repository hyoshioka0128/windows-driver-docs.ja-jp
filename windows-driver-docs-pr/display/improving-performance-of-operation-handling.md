---
title: 操作処理のパフォーマンスの向上
description: 操作処理のパフォーマンスの向上
ms.assetid: 14b5aa90-15ee-40c6-8f5b-e776b07932ab
keywords:
- Direct3D WDK Windows 2000 の表示、操作コード
- 操作コード WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1675253e8379b11b4041b6b20e599d9e978413ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383934"
---
# <a name="improving-performance-of-operation-handling"></a>操作処理のパフォーマンスの向上


## <span id="ddk_improving_performance_of_operation_handling_gg"></span><span id="DDK_IMPROVING_PERFORMANCE_OF_OPERATION_HANDLING_GG"></span>


ディスプレイ ドライバーのパフォーマンスを向上させるには、グラフィックス プリミティブを描画および状態の変更の処理は、ドライバーを実装するときに、次のものを確認する必要があります。

-   DirectX のランタイムは、レンダリング状態パラメーターを設定する冗長な要求をフィルター処理します。 つまり、アプリケーションを呼び出す場合、 **IDirect3DDevice8::SetRenderState**メソッドを複数回冗長な呼び出し、およびドライバーのシーンをレンダリングする前に、同じデバイスレンダリング状態パラメーターを設定するに、ランタイムをフィルター処理[**D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数はこの特定のレンダリング状態パラメーターを設定する 1 つの要求のみを受け取ります。 そのため、このフィルター アクションを実行するには、ドライバーを実装することはありません。

-   操作要求を受け取るたびにしないとプリミティブを描画する前に、ドライバーはレンダリング状態レジスタに書き込むだけする必要があります ([**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation))。

詳細については**IDirect3DDevice8::SetRenderState**、Direct3D SDK のドキュメントを参照してください。

 

 





