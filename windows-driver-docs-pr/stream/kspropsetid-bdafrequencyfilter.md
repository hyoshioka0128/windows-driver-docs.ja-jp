---
title: KSPROPSETID\_BdaFrequencyFilter
description: KSPROPSETID\_BdaFrequencyFilter
ms.assetid: 7650a239-3d49-4cb1-99bb-12bac55d70d2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ced82098e7dc6dd5deaf0c711266ec0b2463ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389231"
---
# <a name="kspropsetidbdafrequencyfilter"></a>KSPROPSETID\_BdaFrequencyFilter


## <span id="ddk_kspropsetid_bdafrequencyfilter_ks"></span><span id="DDK_KSPROPSETID_BDAFREQUENCYFILTER_KS"></span>


KSPROPSETID\_BdaFrequencyFilter は BDA 周波数のフィルターのプロパティ セット。 受信者のトポロジで RF チューナー ノードの制御に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY"></span><span id="ksproperty_bda_rf_tuner_frequency"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_頻度**](ksproperty-bda-rf-tuner-frequency.md)  
チューナー ノード シグナル キャリアの基本の周波数を通知します。 基本の頻度を KSPROPERTY の値に乗算\_BDA\_RF\_チューナー\_頻度\_乗数のプロパティを実際の頻度を取得します。

<span id="KSPROPERTY_BDA_RF_TUNER_POLARITY"></span><span id="ksproperty_bda_rf_tuner_polarity"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_極性**](ksproperty-bda-rf-tuner-polarity.md)  
極性送信信号で使用されるチューナー ノードを通知します。

<span id="KSPROPERTY_BDA_RF_TUNER_RANGE"></span><span id="ksproperty_bda_rf_tuner_range"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_範囲**](ksproperty-bda-rf-tuner-range.md)  
チューナーの範囲を設定します。

<span id="KSPROPERTY_BDA_RF_TUNER_TRANSPONDER"></span><span id="ksproperty_bda_rf_tuner_transponder"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_トランスポンダー**](ksproperty-bda-rf-tuner-transponder.md)  
適切なトランスポンダー数のチューナーのノードに通知します。

<span id="KSPROPERTY_BDA_RF_TUNER_BANDWIDTH"></span><span id="ksproperty_bda_rf_tuner_bandwidth"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_帯域幅**](ksproperty-bda-rf-tuner-bandwidth.md)  
送信信号の帯域幅のチューナーのノードに通知します。

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER"></span><span id="ksproperty_bda_rf_tuner_frequency_multiplier"></span>[**KSPROPERTY\_BDA\_RF\_チューナー\_頻度\_乗数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)  
チューナー ノードに通知する、KSPROPERTY の値に乗算する値\_BDA\_RF\_チューナー\_頻度プロパティを実際の頻度を取得します。

### <a name="comments"></a>コメント

KSPROPSETID\_BdaFrequencyFilter プロパティ セットは、ほぼすべてのチューナーの間でジェネリック。 チューナー ノード、RF 信号をチューニングする方法を通知するために使用されます。

 

 





