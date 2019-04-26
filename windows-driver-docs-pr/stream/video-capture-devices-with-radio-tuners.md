---
title: ラジオ チューナー付きビデオ キャプチャ デバイス
description: ラジオ チューナー付きビデオ キャプチャ デバイス
ms.assetid: 36e3ca98-cb1b-46cc-809a-8c9ad08a53c8
keywords:
- ラジオ チューナー WDK ビデオのキャプチャします。
- PLL オフセット WDK ビデオのキャプチャ
- 信号強度 WDK ビデオのキャプチャ
- 手動のラジオ WDK ビデオ キャプチャのチューニング
- FM チューナー WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0516b11d079e4bdda6d2c03a9cf6dd4323f3764
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351601"
---
# <a name="video-capture-devices-with-radio-tuners"></a>ラジオ チューナー付きビデオ キャプチャ デバイス


Microsoft Windows XP 以降では、8.1 以降の Microsoft DirectX は FM を含むビデオ キャプチャ デバイス ラジオ チューナーのサポートを提供します。

FM チューナーを使用したデバイスのビデオ キャプチャ ミニドライバーをサポートする必要があります、 [ **KSPROPERTY\_チューナー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff565921)プロパティ。 これにより、ユーザー モードのクライアントを取得する、 [ **KSPROPERTY\_チューナー\_状態\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565925)チューニング操作の進行状況を記述する構造体。

ミニドライバーは、次の 3 つのチューニング方法のいずれかをサポートできます。

1.  **PLL オフセットをチューニングします。**

    FM チューナー ハードウェアが PLL オフセットでチューニングをサポートする場合、ミニドライバーを設定する必要があります、**戦略**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_キャップ\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872) KS 構造\_チューナー\_戦略\_PLL します。

    FM チューナー ハードウェアが PLL サポートを提供していない場合、ミニドライバーは、ネイティブの信号強度インジケーターを使用して PLL サポートをエミュレートする必要があります。 チューニングでは、ロジック、システム提供の FM *KsTvTune.ax* 、ミニドライバーの指定をサポートしている場合にのみ有効です、 **KS\_チューナー\_戦略\_PLL**戦略。

2.  **信号の強さをチューニングします。**

    ミニドライバーが設定されている場合、**戦略**、KSPROPERTY のメンバー\_チューナー\_モード\_CAP\_KS S 構造\_チューナー\_戦略\_信号\_強度、 *KsTvTune.ax*を使用しようとしても、 **PLLOffset** 、KSPROPERTY のメンバー\_チューナー\_状態\_S 構造体。 したがって、将来の互換性の有効なオプションではありません。

    さらに、ミニドライバーを設定する必要があります、 **SignalStrength**のメンバー、 [ **KSPROPERTY\_チューナー\_状態\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565925)-1、0、または 1 の許容される頻度が現在選択されているかどうかに応じて、構造体。 ベンダーは、受信者信号強度指標 (RSSI) またはデシベル読み書き可能 (dBmV) レベルの上または下ベースライン電圧 FM 受信のため、許容される信号の構成要素を決定します。

3.  **チューニングは、ミニドライバーによって手動で実行されます。**

    設定、**戦略**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872) 構造体**KS\_チューナー\_戦略\_ドライバー\_チューニング**コントロール、ミニドライバーのロジックを調整します。

FM のモードで*KsTvTune.ax*頻度 (右辺でも左辺でも 100 kHz)、200 kHz バンドをステップ実行ミニドライバー指定を使用して**TuningGranularity**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)ステップ サイズとして構造体。 検索を停止した*KsTvTune.ax*全体の 200 kHz バンドの検索が、ミニドライバーが良好な信号が見つかったこと、早い方を判断するとき、または。

チューニングが長く、ミニドライバーは常に指定されている場合、 **PLLOffset** -1 または 1 の値。 この場合は、チューニングのロジックで*KsTvTune.ax*再試行の頻度の範囲が重複します。 ミニドライバーを指定する必要があります、 **PLLOffset** -1 または 1、チューニングの最初の要求でのみ、またはチューナーが 8 つの手順の最適な信号内の。 要求のチューニングの詳細については、次を参照してください。[最初のチューニング要求を認識する](recognizing-the-first-tuning-request.md)します。

チューニング処理は常に、アプリケーションによって要求された center 頻度、開始し、中央上 kHz が 100 以上手順します。 ただし場合、 **PLLOffset** 100 kHz バンド以外のチューニング ロジック手順 1、上限 100 kHz の近くになります。

チューニング処理が上の範囲で、許容可能な信号を見つけられない場合は、以下の中心周波数、中央下 kHz が 100 を下回ってからステップ実行と、まだが検出されない場合許容可能なシグナルの中心周波数終了試みます。 ここでも場合、 **PLLOffset**中心周波数以外に手順を最後にそれを返す前にチューニング center 頻度は、ほぼ 1 になります。

A **PLLOffset** -1 または 1 で最初のチューニングのメンバー値要求エラーの原因*KsTvTune.ax*調整モードを入力します。 指定されたステップの間隔で立て続けに要求をチューニングは、調整モード、 **TuningGranularity**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)によって示される方向構造**PLLOffset**します。

*KsTvTune.ax*それが成功しなかった場合、昇順または頻度を減らす微調整 8 つの手順の後に、チューニングの試行を停止します。 後*KsTvTune.ax*モードを微調整する場合は、 **PLLOffset** 0、-1 から 1、または-1 に 1 方向を変更またはチューニングの要求が成功と見なされます。 調整と 200 kHz 帯域内で検索をその時点で停止します。

ただし場合、 **PLLOffset**が 1 または-1 より小さい場合よりも大きいの微調整が起動しない、または破棄されます。 指定されたステップ サイズを使用して、両方が、調整モードは、200 kHz バンド center 頻度、検索の独立した**TuningGranularity** (常に返すに対する注意ではそのため、 **PLLOffset** 1..1 の)。

 

 




