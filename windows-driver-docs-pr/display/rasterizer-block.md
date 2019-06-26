---
title: ラスタライザー ブロック
description: ラスタライザー ブロック
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed23f122fb8a13fb17d175d2b9f9f660e94705eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385035"
---
# <a name="rasterizer-block"></a>ラスタライザー ブロック


ラスタライザー ブロックは、クリップ、プリミティブを設定し、ピクセル シェーダーのステージを呼び出す方法を決定します。 Direct3D のランタイムでは、パイプラインのステージとしてラスタライザー ブロックは表示されません。 代わりに、Direct3D のランタイムは、重要な固定機能の操作を実行するために発生するパイプライン ステージの間のインターフェイスとしてラスタライザーのブロックを表示します。 これらの固定機能操作の多くは、ソフトウェア開発者が調整できます。

ラスタライザー常に判断入力位置クリップ空間に用意されて、クリッピングとパースペクティブの除算を実行し、ビューポートのスケールとオフセットが適用されます。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ラスタライザーの状態を破棄します。

[**CalcPrivateRasterizerStateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivaterasterizerstatesize)

[**CreateRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createrasterizerstate)

[**DestroyRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyrasterizerstate)

[**SetRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setrasterizerstate)

[**SetScissorRects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setscissorrects)

[**SetViewports**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setviewports)

 

 





