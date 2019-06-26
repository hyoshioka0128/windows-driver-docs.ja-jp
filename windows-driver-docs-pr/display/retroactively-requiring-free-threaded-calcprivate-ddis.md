---
title: フリー スレッド CalcPrivate DDI が遡及的に必要
description: フリー スレッド CalcPrivate DDI が遡及的に必要
ms.assetid: a25fbe8e-737a-4b47-8293-7cf13ebc8ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7712e88eb798376fba0cdec4b28c13ab9c10b0ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365640"
---
# <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>フリー スレッド CalcPrivate DDI が遡及的に必要


始まる Direct3D のバージョン 11 は、ユーザー モードのディスプレイ ドライバー関数過去にさかのぼってが必要です。 *pfnCalcPrivate*フリー スレッドである Direct3D バージョン 10 DDI 関数。 この事後対応の要件に一致する Direct3D のバージョン 11 の動作を常に必要とする DDI *pfnCalcPrivate\** と[ **pfnCalcDeferredContextHandleSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)はフリー スレッド場合でも、ドライバーでは、そのことを示します関数は DDI スレッド処理をサポートしていません。 ドライバーを示す方法の詳細についてはスレッドのサポートを参照してください[スレッド処理をサポートしている、コマンドを一覧表示、および 3-D パイプライン](supporting-threading--command-lists--and-3-d-pipeline.md)します。 この事後対応要件の理由は、サイズの即時の値を返すには、このような関数は非常にシンプル通常ことです。 複雑な関数では、関数に渡されるパラメーターに基づいて、どのイミディ エイト値を返すを決定します。 始まる関数の要件*pfnCalcPrivate*実際にデータを書き込む場所を他にも、スタックは存在しません。 これらの関数のパラメーター以外のデータを読み取るための要件は、珍しいものです。 データの読み取りに必要では、競合の問題は発生しません。 この事実をはるかに必要な最適化を受け取り、作成するごとに 2 回の高価な同期を実行できないようにする Direct3D のバージョン 11 API は、(たとえば、すべての呼び出しへの呼び出しのようなオブジェクトを作成する[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)または[ **CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader))、1 回だけではなく。

この事後対応のフリー スレッド要件に注目すべき例外は、 [ **CalcPrivateDeviceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)ディスプレイ デバイスの作成を満たすために使用される関数です。 *CalcPrivateDeviceSize*アダプターは、関数テーブル上にある ([**D3D10\_2DDI\_ADAPTERFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)または[ **D3D10DDI\_ADAPTERFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_adapterfuncs))。 *CalcPrivateDeviceSize*スレッド モデルで緩和したトークンが発生した関数のグループの下にあることはありません。 複数のスレッドが解放する必要はありません、 *CalcPrivateDeviceSize*関数。

 

 





