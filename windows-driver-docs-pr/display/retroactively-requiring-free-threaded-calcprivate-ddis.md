---
title: 過去にさかのぼって、フリー スレッド CalcPrivate Ddi を必要とします。
description: 過去にさかのぼって、フリー スレッド CalcPrivate Ddi を必要とします。
ms.assetid: a25fbe8e-737a-4b47-8293-7cf13ebc8ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f86c42e4d48c676424e03faa050db1fa27839eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559589"
---
# <a name="retroactively-requiring-free-threaded-calcprivate-ddis"></a>過去にさかのぼって、フリー スレッド CalcPrivate Ddi を必要とします。


始まる Direct3D のバージョン 11 は、ユーザー モードのディスプレイ ドライバー関数過去にさかのぼってが必要です。 *pfnCalcPrivate*フリー スレッドである Direct3D バージョン 10 DDI 関数。 この事後対応の要件に一致する Direct3D のバージョン 11 の動作を常に必要とする DDI *pfnCalcPrivate\** と[ **pfnCalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)はフリー スレッド場合でも、ドライバーでは、そのことを示します関数は DDI スレッド処理をサポートしていません。 ドライバーを示す方法の詳細についてはスレッドのサポートを参照してください[スレッド処理をサポートしている、コマンドを一覧表示、および 3-D パイプライン](supporting-threading--command-lists--and-3-d-pipeline.md)します。 この事後対応要件の理由は、サイズの即時の値を返すには、このような関数は非常にシンプル通常ことです。 複雑な関数では、関数に渡されるパラメーターに基づいて、どのイミディ エイト値を返すを決定します。 始まる関数の要件*pfnCalcPrivate*実際にデータを書き込む場所を他にも、スタックは存在しません。 これらの関数のパラメーター以外のデータを読み取るための要件は、珍しいものです。 データの読み取りに必要では、競合の問題は発生しません。 この事実をはるかに必要な最適化を受け取り、作成するごとに 2 回の高価な同期を実行できないようにする Direct3D のバージョン 11 API は、(たとえば、すべての呼び出しへの呼び出しのようなオブジェクトを作成する[ **CreateResource(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540691)または[ **CreateGeometryShader**](https://msdn.microsoft.com/library/windows/hardware/ff540648))、1 回だけではなく。

この事後対応のフリー スレッド要件に注目すべき例外は、 [ **CalcPrivateDeviceSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538288)ディスプレイ デバイスの作成を満たすために使用される関数です。 *CalcPrivateDeviceSize*アダプターは、関数テーブル上にある ([**D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)または[ **D3D10DDI\_ADAPTERFUNCS**](https://msdn.microsoft.com/library/windows/hardware/ff541811))。 *CalcPrivateDeviceSize*スレッド モデルで緩和したトークンが発生した関数のグループの下にあることはありません。 複数のスレッドが解放する必要はありません、 *CalcPrivateDeviceSize*関数。

 

 





