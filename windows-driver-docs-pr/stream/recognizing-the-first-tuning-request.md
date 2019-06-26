---
title: 最初のチューニング要求の認識
description: 最初のチューニング要求の認識
ms.assetid: dc18a056-16f8-4b99-97e3-52c92464a2b2
keywords:
- 最初のチューニング要求 WDK ビデオのキャプチャします。
- 最初チューニング要求 WDK ビデオのキャプチャを認識します。
- ラジオ チューナー WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4cc6b83018a018b53f2fbb524f29985a2ecc62a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366497"
---
# <a name="recognizing-the-first-tuning-request"></a>最初のチューニング要求の認識


ミニドライバーは、タイミングを認識する必要があります、有効な信号強度/PLL 情報を取得する頻度を高速移動のチューナーを必要と*KsTvTune.ax*は初期のチューニングの要求を行っています。

チューニングの各要求は、実際には、ミニドライバーに要求のペアです。 最初に、ミニドライバーは、セットを受信[ **KSPROPERTY\_チューナー\_頻度**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency)後に 1 つまたは複数の get 要求[ **KSPROPERTY\_チューナー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)要求。

最初のチューニングの要求では、セットの要求と、最初の get 要求の間の遅延です。 ミニドライバーではミリ秒単位の遅延の長さの設定、 **SettlingTime**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体。 Get 要求を繰り返し中には 5 ミリ秒ごと、**ビジー**のメンバー、 [ **KSPROPERTY\_チューナー\_状態\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)構造が 0 以外で、最大で 5 つの試行します。

*KsTvTune.ax*は考慮されません調整要求完了 nonbusy ステータス、デバイスから受信するまで、またはデバイスがまだ使用中の 20 ミリ秒の場合、によって指定された期間後、 **SettlingTime**のメンバー、[ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体のどちらか早い。

その後、調整モード中にチューニング要求ごとがある 5 ミリ秒間隔設定要求の間と、最初の要求を取得します。

場合*KsTvTune.ax*最初の要求後に 1 回以上再試行は、常に返す、 **PLLOffset**チューニングの最初の要求で 1 の値。 *KsTvTune.ax*以上で指定したとおり、次の手順をすぐに試行、 **TuningGranularity**のメンバー、 [ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体。 その時点で返すことができますが、 **PLLOffset** 1 または-1、ミニドライバーの信号がないと判断した場合より小さい値より大きい値または**PLLOffset**値-1 または 0、ミニドライバーが判断した場合、シグナルをお勧めします。

 

 




