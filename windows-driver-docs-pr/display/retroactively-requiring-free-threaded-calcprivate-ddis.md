---
title: フリー スレッド CalcPrivate DDI が遡及的に必要
description: フリー スレッド CalcPrivate DDI が遡及的に必要
ms.assetid: a25fbe8e-737a-4b47-8293-7cf13ebc8ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fae5c82495d0b922db8187a7294e4e67cc4e0e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829571"
---
# <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>フリー スレッド CalcPrivate DDI が遡及的に必要


Direct3D バージョン11以降では、フリースレッドの Direct3D バージョン 10 DDI 関数の*pfnCalcPrivate*で始まるユーザーモードの表示ドライバー関数が必要です。 この遡及的要件は、ドライバーではないと示されていても、 *pfnCalcPrivate\** および[**pfnCalcDeferredContextHandleSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)関数を常に必要とする Direct3D バージョン 11 DDI の動作と一致します。DDI スレッド処理をサポートします。 ドライバーがスレッド処理のサポートを示す方法の詳細については、「[スレッド処理、コマンド一覧、および3-D パイプラインのサポート](supporting-threading--command-lists--and-3-d-pipeline.md)」を参照してください。 この遡及的要件の理由は、通常、このような関数はサイズのイミディエイト値を返すため、非常に単純です。 より複雑な関数は、関数に渡されるパラメーターに基づいてどのイミディエイト値を返すかを決定します。 スタック以外の場所にデータを実際に書き込むために*pfnCalcPrivate*で始まる関数の要件は存在しません。 これらの関数がパラメーター以外のデータを読み取るための要件は、rarity ティです。 データを読み取る必要がある場合、競合の問題は発生しません。 これにより、Direct3D バージョン 11 API は必要な最適化を大幅に実行できるようになり、1つの作成に対してコストの高い同期が2回実行されるのを防ぐことができます (たとえば、 [**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)の呼び出しなどのオブジェクトを作成する呼び出しなど)。 [**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)) を1回だけ実行するのではなく、

この遡及的フリースレッド要件の注目すべき例外は、ディスプレイデバイスの作成を満たすために使用される[**CalcPrivateDeviceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)関数です。 *CalcPrivateDeviceSize*は、アダプター関数テーブル ([**D3D10\_2DDI\_Adapterfuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)または[**D3D10DDI\_adapterfuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_adapterfuncs)) にあります。 *CalcPrivateDeviceSize*は、スレッドモデルで緩和を経験した関数のグループの下には含まれません。 *CalcPrivateDeviceSize*関数を解放する必要はありません。

 

 





