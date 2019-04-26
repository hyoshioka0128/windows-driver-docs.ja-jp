---
title: 出力結合 (OM) ステージ
description: 出力結合 (OM) ステージ
ms.assetid: 9b549614-0f51-4c79-a6c4-ba907a5f9068
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de6b397b57ae785c386d2aabc7c5a023ad44df8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358348"
---
# <a name="output-merger-stage"></a>出力結合 (OM) ステージ


論理のパイプラインの最後の手順では、ステンシルまたは深さを記述または出力のブレンド経由の可視性決定、多くのリソースの種類のいずれかのターゲットを表示するためにです。 出力 (レンダー ターゲット) のリソースのバインドと同様に、これらの操作は、出力マージャー ステージで定義されます。

Direct3D ランタイムでは、次のドライバー関数を作成、設定、消去、および、出力の破棄を呼び出します。

[**CalcPrivateBlendStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538274)

[**CalcPrivateDepthStencilStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538282)

[**CalcPrivateDepthStencilViewSize**](https://msdn.microsoft.com/library/windows/hardware/ff538284)

[**ClearDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff539408)

[**ClearRenderTargetView**](https://msdn.microsoft.com/library/windows/hardware/ff539409)

[**CreateBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff540594)

[**CreateDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff540627)

[**CreateDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff540629)

[**DestroyBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff552745)

[**DestroyDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff552759)

[**DestroyDepthStencilView**](https://msdn.microsoft.com/library/windows/hardware/ff552762)

[**SetBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff569527)

[**SetDepthStencilState**](https://msdn.microsoft.com/library/windows/hardware/ff569532)

[**SetPredication**](https://msdn.microsoft.com/library/windows/hardware/ff569547)

[**SetRenderTargets**](https://msdn.microsoft.com/library/windows/hardware/ff569553)

[**SetTextFilterSize**](https://msdn.microsoft.com/library/windows/hardware/ff569663)

 

 





