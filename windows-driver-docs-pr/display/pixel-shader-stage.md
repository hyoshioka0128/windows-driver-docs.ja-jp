---
title: ピクセル シェーダーのステージ
description: ピクセル シェーダーのステージ
ms.assetid: 969b6cb9-7b03-4c9f-bf4a-e8d9b442c847
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ec1c0e0bdda7e7a246b332bf2075af41caf72b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531437"
---
# <a name="pixel-shader-stage"></a>ピクセル シェーダーのステージ


ピクセル シェーダーのステージで使用可能な入力データには、頂点属性に選択できる、要素ごとに、パースペクティブの修正の有無を挿入するのには、プリミティブ単位の定数として扱われますが含まれています。

出力は、(、ピクセルは破棄されます) 場合は、現在のピクセルの場所の出力データの 1 つ以上 4 ベクトルまたは色なしです。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ピクセル シェーダーを破棄します。

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CreatePixelShader(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540670)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**PsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff569207)

[**PsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff569208)

[**PsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff569209)

[**PsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff569210)

 

 





