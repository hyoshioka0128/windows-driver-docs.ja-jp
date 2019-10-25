---
title: ピクセル シェーダー ステージ
description: ピクセル シェーダー ステージ
ms.assetid: 969b6cb9-7b03-4c9f-bf4a-e8d9b442c847
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb2cc1628ad088336fb36f8393f1fcc1663496e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829800"
---
# <a name="pixel-shader-stage"></a>ピクセル シェーダー ステージ


ピクセルシェーダーステージで使用できる入力データには、要素ごとに選択できる頂点属性が含まれています。これらの属性は、パースペクティブ修正の有無にかかわらず補間したり、プリミティブごとに定数として処理したりすることができます。

出力は、現在のピクセル位置の出力データの1つ以上の4ベクトルです。または、色がありません (ピクセルが破棄されている場合)。

Direct3D ランタイムは、次のドライバー関数を呼び出して、ピクセルシェーダーを作成、設定、および破棄します。

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreatePixelShader (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createpixelshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**PsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**PsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**PsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**PsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





