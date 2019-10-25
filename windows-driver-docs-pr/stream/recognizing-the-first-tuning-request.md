---
title: 最初のチューニング要求の認識
description: 最初のチューニング要求の認識
ms.assetid: dc18a056-16f8-4b99-97e3-52c92464a2b2
keywords:
- 最初のチューニング要求 WDK ビデオキャプチャ
- 最初のチューニング要求を認識する WDK ビデオキャプチャ
- ラジオチューナー WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f728c94ae3286224d5c8725d932ed902c9a3be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841661"
---
# <a name="recognizing-the-first-tuning-request"></a>最初のチューニング要求の認識


チューナーによっては、信号強度/PLL の有効な情報を取得するために周波数を調整する必要があるため、 *KsTvTune.ax*が最初のチューニング要求を行ったときに、ミニドライバーが認識する必要がある場合があります。

各チューニング要求は、実際にはミニドライバーに対する要求のペアです。 最初のミニドライバーは、 [ **\_チューナー\_FREQUENCY**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency)要求の後に1つ以上の Get [**ksproperty\_チューナー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)要求を受け取ります。

最初のチューニング要求では、設定要求と最初の get 要求の間に遅延があります。 ミニドライバーは、 [ **\_チューナー\_モード\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体の、ksk プロパティの**sett time**メンバーの遅延時間をミリ秒単位で設定します。 Get 要求は5ミリ秒ごとに繰り返されますが、 [**Ksk プロパティ\_チューナー\_ステータス\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)構造体の**ビジー状態**のメンバーは0以外で、最大で5回試行されます。

*KsTvTune.ax*は、デバイスから使用されていない状態を受信するまで、またはデバイスが Ksk\_プロパティの**sett time**メンバーによって指定された期間が経過しても20ミリ秒後にビジー状態になるまで、チューニング要求を完了しません。 [**チューナー\_モード\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体のいずれか早い方です。

その後、微調整モード中の各チューニング要求では、set 要求と最初の get 要求の間に5ミリ秒の間隔が設定されます。

最初の要求の後に*KsTvTune.ax*が少なくとも1回再試行されるようにする場合は、最初のチューニング要求で常に**plloffset**値1を返します。 *KsTvTune.ax*は、 [**KSK プロパティ\_チューナー\_MODE\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体の**tuninggranularity 度**メンバーによって指定されている次のステップを直ちに再試行します。 その時点で、ミニドライバーが1より大きいか、または-1 より小さい**Plloffset**値を返すことができます。これは、シグナルがないと判断した場合、またはミニドライバーによって信号が良好であると判断された場合に、 **plloffset**値が-1 または0になります。

 

 




