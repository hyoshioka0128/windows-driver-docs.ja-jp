---
title: ラスタライザーのブロック
description: ラスタライザーのブロック
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08364909ef7f3bd3075ef83b04314e5e5d377b24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560196"
---
# <a name="rasterizer-block"></a>ラスタライザーのブロック


ラスタライザー ブロックは、クリップ、プリミティブを設定し、ピクセル シェーダーのステージを呼び出す方法を決定します。 Direct3D のランタイムでは、パイプラインのステージとしてラスタライザー ブロックは表示されません。 代わりに、Direct3D のランタイムは、重要な固定機能の操作を実行するために発生するパイプライン ステージの間のインターフェイスとしてラスタライザーのブロックを表示します。 これらの固定機能操作の多くは、ソフトウェア開発者が調整できます。

ラスタライザー常に判断入力位置クリップ空間に用意されて、クリッピングとパースペクティブの除算を実行し、ビューポートのスケールとオフセットが適用されます。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ラスタライザーの状態を破棄します。

[**CalcPrivateRasterizerStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538298)

[**CreateRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff540676)

[**DestroyRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff552788)

[**SetRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff569550)

[**SetScissorRects**](https://msdn.microsoft.com/library/windows/hardware/ff569659)

[**SetViewports**](https://msdn.microsoft.com/library/windows/hardware/ff569698)

 

 





