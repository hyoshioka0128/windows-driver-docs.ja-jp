---
title: プリミティブ描画と状態変更
description: プリミティブ描画と状態変更
ms.assetid: 01eba14d-234e-48f5-9116-47760dfdae0e
keywords:
- Direct3D WDK Windows 2000 の表示、プリミティブを描画
- Direct3D WDK Windows 2000 の表示、状態の変更
- WDK Direct3D を状態します。
- 描画プリミティブの WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 828ca3e214d925e2a153d944cc43a6d1f4460f04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363738"
---
# <a name="primitive-drawing-and-state-changes"></a>プリミティブ描画と状態変更


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


すべてのマイクロソフトの Direct3D グラフィックス プリミティブおよび状態の変更に渡される、 [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンドと頂点バッファーにコールバックします。 ドライバーは、これらのバッファーを解析し、すべての描画と状態変更要求を処理する必要があります。

次のセクションでは、コマンドと頂点バッファーのレイアウトを説明し、ドライバーが処理する方法について説明します。

[コマンドおよび頂点バッファー](command-and-vertex-buffers.md)

[Direct3D コマンド バッファー](direct3d-command-buffers.md)

[Direct3D 頂点バッファー](direct3d-vertex-buffers.md)

[高速化された状態の管理](accelerated-state-management.md)

 

 





