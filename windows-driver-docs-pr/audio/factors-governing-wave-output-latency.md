---
title: Wave 出力の待機時間に影響を及ぼす要因
description: Wave 出力の待機時間に影響を及ぼす要因
ms.assetid: 6342ffd4-b0e8-41a4-ab97-1f658052748b
keywords:
- WDM オーディオ ドライバー WDK、待機時間
- オーディオ ドライバー WDK、待機時間
- wave 出力の待機時間の WDK オーディオ
- 待機時間の WDK オーディオ、wave 出力ストリーム
- 待機時間の WDK オーディオをストリーミングします。
- WDK のオーディオ出力の待機時間
- ハードウェアの待機時間の WDK オーディオ
- ソフトウェアの待機時間の WDK オーディオ
- 混合の待機時間の問題の WDK オーディオ
- DirectSound WDK オーディオ、待機時間
- スタベーション WDK オーディオ
- 時間の WDK オーディオ
- バッファーの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb597f123eaa0992204f0b7125f13fcc389d1598
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333637"
---
# <a name="factors-governing-wave-output-latency"></a>Wave 出力の待機時間に影響を及ぼす要因


## <span id="factors_governing_wave_output_latency"></span><span id="FACTORS_GOVERNING_WAVE_OUTPUT_LATENCY"></span>


このセクションでは、wave 出力ストリームの待機時間のソースについて説明します。 待機時間に影響する要因を次に示します。

-   ストリームの WaveCyclic または WavePci デバイスへの出力がかどうか

-   DirectSound でストリームを生成するかどうか、または**waveOut** API

次のトピックについて説明します。

[WaveCyclic 待機時間](wavecyclic-latency.md)

[WavePci 待機時間](wavepci-latency.md)

[データのコピーを回避します。](avoiding-data-copying.md)

 

 




