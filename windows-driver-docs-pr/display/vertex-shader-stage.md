---
title: 頂点シェーダー ステージ
description: 頂点シェーダー ステージ
ms.assetid: 310ef24a-7647-4f5e-b89f-a3ff330d5df4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2284899f64941949017256b63b0d9286e1d5fb12
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365086"
---
# <a name="vertex-shader-stage"></a>頂点シェーダー ステージ


頂点シェーダー ステージは変換などの操作を実行する、スキン、照明、頂点を処理します。 頂点シェーダーは常に、1 つの入力頂点を処理して 1 つの出力頂点を生成します。 レンダリング パイプラインのこのステージは、常にアクティブである必要があります。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、頂点シェーダーを破棄します。

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateVertexShader(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createvertexshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**VsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**VsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**VsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**VsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





