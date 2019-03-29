---
title: BDA チューナー ノードの周波数プロパティへのアクセス
description: BDA チューナー ノードの周波数プロパティへのアクセス
ms.assetid: 47c24e99-c82c-4bc8-af36-bd7f728634ba
keywords:
- メソッドは、WDK BDA、RF チューナーのノードを設定します。
- プロパティは、WDK BDA、RF チューナーのノードを設定します。
- KSPROPSETID_BdaFrequencyFilter
- RF チューナー WDK BDA
- WDK BDA 周波数のプロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6548a892f7429f6e0eaa4124c2394ebde2ed5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572492"
---
# <a name="accessing-frequency-properties-of-a-bda-tuner-node"></a>BDA チューナー ノードの周波数プロパティへのアクセス





ネットワーク プロバイダーを使用して、 [KSPROPSETID\_BdaFrequencyFilter](https://msdn.microsoft.com/library/windows/hardware/ff566542) BDA フィルター トポロジでは、RF チューナーのノードを制御するプロパティを設定します。 たとえば、ネットワーク プロバイダーは、RF 信号をチューニングする方法をチューナーのノードに通知するためにこのプロパティを使用します。

次のコード スニペットで BDA ミニドライバーのチューナー ノードの制御の暗証番号 (pin) をインターセプトし、KSPROPSETID のプロパティのメソッドを提供\_BdaFrequencyFilter プロパティ セット。 なお一部 KSPROPSETID\_BdaFrequencyFilter プロパティは、チューナーの特定の種類に該当するのみです。

```cpp
//
//  BDA RF Tune Frequency Filter
//
//  Defines the dispatch routines for the Properties
//  on the RF Tuner Node
//
DEFINE_KSPROPERTY_TABLE(RFNodeFrequencyProperties)
{
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_FREQUENCY(
        CAntennaPin::GetCenterFrequency,
        CAntennaPin::PutCenterFrequency
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_FREQUENCY_MULTIPLIER(
        NULL,
        CAntennaPin::PutFrequencyMultiplier // If this set handler 
        // is not called, the minidriver must determine that the 
        // frequency is in kHz. That is, the default multiplier is 
        // 1000 (1Hz x 1000).
        ),
#ifdef SATELLITE_TUNER // Only applicable to satellite tuners.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_POLARITY(
        NULL, NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_RANGE(
        NULL, NULL
        ),
#endif // SATELLITE_TUNER
#ifdef CHANNEL_BASED_TUNER // Only applicable to channel-based tuners.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_TRANSPONDER(
        NULL, NULL
        ),
#endif // CHANNEL_BASED_TUNER
#ifdef DVBT_TUNER // Only applicable to tuners that tune Digital Video Broadcast (DVB) signals.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_BANDWIDTH(
        NULL, NULL
        ),
#endif // DVBT_TUNER
};
```

 

 




