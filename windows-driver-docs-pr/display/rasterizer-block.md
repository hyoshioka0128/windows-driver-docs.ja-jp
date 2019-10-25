---
title: ラスタライザー ブロック
description: ラスタライザー ブロック
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5203d58a17ae4aec5c0a3d704bb1e55b39411cb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825950"
---
# <a name="rasterizer-block"></a>ラスタライザー ブロック


ラスタライザーは、プリミティブを設定し、ピクセルシェーダーステージの呼び出し方法を決定します。 Direct3D ランタイムは、ラスタライザーブロックをパイプラインのステージとして表示しません。 代わりに、Direct3D ランタイムは、一連の固定関数操作を実行するために発生するパイプラインステージ間のインターフェイスとして、ラスタライザーブロックを表示します。 これらの固定関数操作の多くは、ソフトウェア開発者によって調整できます。

ラスタライザーは、入力位置がクリップスペースで提供されることを常に判断し、クリッピングとパースペクティブの分割を実行し、ビューポートのスケールとオフセットを適用します。

Direct3D ランタイムは、次のドライバー関数を呼び出して、ラスタライザーの状態を作成、設定、および破棄します。

[**CalcPrivateRasterizerStateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivaterasterizerstatesize)

[**CreateRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createrasterizerstate)

[**DestroyRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyrasterizerstate)

[**SetRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setrasterizerstate)

[**SetScissorRects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setscissorrects)

[**SetViewports ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setviewports)

 

 





