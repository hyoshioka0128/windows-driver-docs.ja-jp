---
title: プリミティブ描画と状態変更
description: プリミティブ描画と状態変更
ms.assetid: 01eba14d-234e-48f5-9116-47760dfdae0e
keywords:
- Direct3D WDK Windows 2000 display、プリミティブ描画
- Direct3D WDK Windows 2000 の表示、状態の変更
- WDK Direct3D の状態
- プリミティブ描画 WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a015433ab537a58efd550139dbb1895c94d9851
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829701"
---
# <a name="primitive-drawing-and-state-changes"></a>プリミティブ描画と状態変更


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


すべての Microsoft Direct3D グラフィックスプリミティブと状態の変更は、コマンドと頂点バッファーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックに渡されます。 ドライバーは、これらのバッファーを解析し、すべての描画および状態変更要求を処理する必要があります。

次のセクションでは、コマンドと頂点バッファーのレイアウトについて説明し、ドライバーがそれらをどのように処理するかを説明します。

[コマンドと頂点バッファー](command-and-vertex-buffers.md)

[Direct3D コマンドバッファー](direct3d-command-buffers.md)

[Direct3D 頂点バッファー](direct3d-vertex-buffers.md)

[状態管理の高速化](accelerated-state-management.md)

 

 





