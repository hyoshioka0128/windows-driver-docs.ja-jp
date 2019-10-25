---
title: 出力結合 (OM) ステージ
description: 出力結合 (OM) ステージ
ms.assetid: 9b549614-0f51-4c79-a6c4-ba907a5f9068
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332489af6718457188f19172f4034735da34bd08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826114"
---
# <a name="output-merger-stage"></a>出力結合 (OM) ステージ


論理パイプラインの最後の手順は、ステンシルまたは深度を使用した可視性の判定、レンダーターゲットへの出力の書き込みまたはブレンドです。これは、多くのリソースの種類のいずれかになります。 これらの操作、および出力リソース (レンダーターゲット) のバインドは、出力のマージステージで定義されています。

Direct3D ランタイムは次のドライバー関数を呼び出して、出力を作成、設定、クリア、および破棄します。

[**CalcPrivateBlendStateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateblendstatesize)

[**CalcPrivateDepthStencilStateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedepthstencilstatesize)

[**CalcPrivateDepthStencilViewSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedepthstencilviewsize)

[**ClearDepthStencilView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_cleardepthstencilview)

[**ClearRenderTargetView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_clearrendertargetview)

[**CreateBlendState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createblendstate)

[**CreateDepthStencilState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdepthstencilstate)

[**CreateDepthStencilView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdepthstencilview)

[**DestroyBlendState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyblendstate)

[**DestroyDepthStencilState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydepthstencilstate)

[**DestroyDepthStencilView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydepthstencilview)

[**SetBlendState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setblendstate)

[**SetDepthStencilState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setdepthstencilstate)

[**SetPredication**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setpredication)

[**SetRenderTargets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setrendertargets)

[**SetTextFilterSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_settextfiltersize)

 

 





