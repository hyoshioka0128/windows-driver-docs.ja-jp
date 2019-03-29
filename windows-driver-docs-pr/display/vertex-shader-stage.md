---
title: 頂点シェーダー ステージ
description: 頂点シェーダー ステージ
ms.assetid: 310ef24a-7647-4f5e-b89f-a3ff330d5df4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 190afa763f1aca1fb88fd3a3d3c7cb44a6f88cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578435"
---
# <a name="vertex-shader-stage"></a>頂点シェーダー ステージ


頂点シェーダー ステージは変換などの操作を実行する、スキン、照明、頂点を処理します。 頂点シェーダーは常に、1 つの入力頂点を処理して 1 つの出力頂点を生成します。 レンダリング パイプラインのこのステージは、常にアクティブである必要があります。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、頂点シェーダーを破棄します。

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CreateVertexShader(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540720)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**VsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff570573)

[**VsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff570574)

[**VsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff570575)

[**VsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff570576)

 

 





