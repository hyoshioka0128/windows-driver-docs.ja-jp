---
title: KSNODETYPE\_DAC
description: KSNODETYPE\_DAC
ms.assetid: 70b30425-cffc-49e1-aa8b-8f5734bd196e
keywords:
- KSNODETYPE_DAC オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_DAC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38cf31e47ab2f9c0a6583a25daee3d8a320d1fd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333257"
---
# <a name="ksnodetypedac"></a>KSNODETYPE\_DAC


## <span id="ddk_ksnodetype_dac_ks"></span><span id="DDK_KSNODETYPE_DAC_KS"></span>


KSNODETYPE\_DAC のノードがアナログ デジタル コンバーター (DAC) を表します。 DAC のノードには、1 つの入力ストリームと 1 つの出力ストリームがあります。

適切な一般的な規則は、オーディオ ドライバーがそのトポロジ内の 1 つだけの DAC ノードを公開する必要があります。 DirectSound は、ドライバーのトポロジに、1 つの DAC のノードのみが含まれている前提としています、ため、要求を送信スピーカー構成プロパティで検出した最初の DAC のノードには、他のユーザーにありません。 実際には、トポロジを安全に含めることができますのみ、1 つ以上の DAC ノードすべての DAC のノードが同じ物理コントロールを表す場合。 すべての DAC のノードで同じプロパティの設定の効果がここが DAC のノードのいずれかのプロパティを設定します。 オーディオ ドライバーが Windows での問題を回避する Me DAC の複数のノードを使用する必要があります/98、Windows 2000、および Windows XP:ミニポート ドライバーでは、1 つ以上のウェーブ レンダリング暗証番号 (pin) ファクトリを提供し、これらのピン フィードを DAC のノードの合計ノードをまとめてからストリームが混在するトポロジを持つ場合、wdmaud.drv (ミキサー行ドライバー) が誤って報告される個別のウェーブ ボリューム コントロール暗証番号 (pin) ファクトリごとにします。 1 つのウェーブ ボリューム コントロールのみを生成します。 この問題を解決するには、回避ソリューションは、各ピン ファクトリからのデータ パスに DAC のノードを挿入すること。

KSNODETYPE\_DAC のノードは、次の省略可能なプロパティをサポートできます。

[**KSPROPERTY\_オーディオ\_チャネル\_構成**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_オーディオ\_動的\_サンプリング\_率**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY\_オーディオ\_サンプリング\_率**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY\_AUDIO\_STEREO\_SPEAKER\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

 

 





