---
title: 操作処理のパフォーマンスの向上
description: 操作処理のパフォーマンスの向上
ms.assetid: 14b5aa90-15ee-40c6-8f5b-e776b07932ab
keywords:
- Direct3D WDK Windows 2000 display、操作コード
- 操作コード WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cdc6b0c58518b49e20f0493bfd5f6a1bc0d296d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840383"
---
# <a name="improving-performance-of-operation-handling"></a>操作処理のパフォーマンスの向上


## <span id="ddk_improving_performance_of_operation_handling_gg"></span><span id="DDK_IMPROVING_PERFORMANCE_OF_OPERATION_HANDLING_GG"></span>


ディスプレイドライバーのパフォーマンスを向上させるには、ドライバーを実装してグラフィックスプリミティブをレンダリングし、状態の変更を処理するときに、次の項目を確認する必要があります。

-   DirectX ランタイムは、冗長な要求をフィルター処理して、レンダリング状態パラメーターを設定します。 つまり、アプリケーションが**IDirect3DDevice8:: SetRenderState**メソッドを複数回呼び出して、シーンをレンダリングする前に同じデバイスのレンダリング状態パラメーターを設定した場合、ランタイムは冗長な呼び出しを除外し、ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数は、この特定のレンダリング状態パラメーターを設定するために1つの要求のみを受け取ります。 このため、このフィルター処理を実行するためにドライバーを実装する必要はありません。

-   ドライバーは、操作要求 ([**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)) を受け取るたびにではなく、プリミティブを描画する直前にレンダリング状態レジスタに書き込む必要があります。

**IDirect3DDevice8:: SetRenderState**の詳細については、Direct3D SDK のドキュメントを参照してください。

 

 





