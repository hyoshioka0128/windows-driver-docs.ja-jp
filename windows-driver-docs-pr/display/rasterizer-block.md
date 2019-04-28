---
title: ラスタライザー ブロック
description: ラスタライザー ブロック
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08364909ef7f3bd3075ef83b04314e5e5d377b24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372985"
---
# <a name="rasterizer-block"></a>ラスタライザー ブロック


ラスタライザー ブロックは、クリップ、プリミティブを設定し、ピクセル シェーダーのステージを呼び出す方法を決定します。 Direct3D のランタイムでは、パイプラインのステージとしてラスタライザー ブロックは表示されません。 代わりに、Direct3D のランタイムは、重要な固定機能の操作を実行するために発生するパイプライン ステージの間のインターフェイスとしてラスタライザーのブロックを表示します。 これらの固定機能操作の多くは、ソフトウェア開発者が調整できます。

ラスタライザー常に判断入力位置クリップ空間に用意されて、クリッピングとパースペクティブの除算を実行し、ビューポートのスケールとオフセットが適用されます。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ラスタライザーの状態を破棄します。

[**CalcPrivateRasterizerStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538298)

[**CreateRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff540676)

[**DestroyRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff552788)

[**SetRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff569550)

[**SetScissorRects**](https://msdn.microsoft.com/library/windows/hardware/ff569659)

[**SetViewports**](https://msdn.microsoft.com/library/windows/hardware/ff569698)

 

 





