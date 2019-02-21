---
title: プリミティブの描画と状態の変更
description: プリミティブの描画と状態の変更
ms.assetid: 01eba14d-234e-48f5-9116-47760dfdae0e
keywords:
- Direct3D WDK Windows 2000 の表示、プリミティブを描画
- Direct3D WDK Windows 2000 の表示、状態の変更
- WDK Direct3D を状態します。
- 描画プリミティブの WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bac427081e1d5c9a7d43e6e1f7ef23fc17f6763
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535513"
---
# <a name="primitive-drawing-and-state-changes"></a>プリミティブの描画と状態の変更


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


すべてのマイクロソフトの Direct3D グラフィックス プリミティブおよび状態の変更に渡される、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コマンドと頂点バッファーにコールバックします。 ドライバーは、これらのバッファーを解析し、すべての描画と状態変更要求を処理する必要があります。

次のセクションでは、コマンドと頂点バッファーのレイアウトを説明し、ドライバーが処理する方法について説明します。

[コマンドおよび頂点バッファー](command-and-vertex-buffers.md)

[Direct3D コマンド バッファー](direct3d-command-buffers.md)

[Direct3D 頂点バッファー](direct3d-vertex-buffers.md)

[高速化された状態の管理](accelerated-state-management.md)

 

 





