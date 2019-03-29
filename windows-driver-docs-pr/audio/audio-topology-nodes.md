---
title: オーディオ トポロジ ノード
description: オーディオ トポロジ ノード
ms.assetid: d999955b-d620-41c9-b42d-6870ce1d4b93
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8984a5e2436ea38b954d148dec4949e11f1387
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578830"
---
# <a name="audio-topology-nodes"></a>オーディオ トポロジ ノード


## <span id="ddk_audio_topology_nodes_ks"></span><span id="DDK_AUDIO_TOPOLOGY_NODES_KS"></span>


WDM オーディオ ドライバー、フレームワークでは、オーディオ デバイスのトポロジのノードの標準セットを定義します。 ミニポート ドライバーでは、一連のノードとノード間の接続を指定することで、デバイスのオーディオのトポロジについて説明します。 [SysAudio システム ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver)この情報を使用して、クライアント アプリケーションに提示されているオーディオ フィルター グラフを作成します。

トポロジ内の各データ パスを開始または停止、pin といくつかのノードを通過ですることができますと見なすデータ パスに沿った一ビーズします。 データ パス内の各ノードは、データ パス内でそのノードを一意に識別するノード ID (基本的にはインデックス) によって識別されます。 暗証番号 (pin) の 2 つのインスタンスが同じ ID を持つノードを持つ可能性がありますが、暗証番号 (pin) のインスタンスとノードの ID の組み合わせは、オーディオ、トポロジ内の各ノードを一意に識別します。

トポロジのノードには、一連のノード プロパティがサポートしています。 ノードのプロパティは、プロパティが属する内部ノードを識別するノード ID を含めることで pin のプロパティとは異なります。 特定のノードに get または set プロパティの要求を送信するには、クライアントは、ターゲット暗証番号 (pin) のインスタンスだけでなく、ターゲット ノードの ID を指定します。 暗証番号 (pin) のプロパティのハンドラーは、要求を受け取るノード ID で検索し、そのノードのハンドラーに要求を送信します。

次の一覧には、一般的に使用されるオーディオのトポロジ ノードの種類が含まれています。

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_AUDIO\_ENGINE**](ksnodetype-audio-engine.md)

[**KSNODETYPE\_AUDIO\_KEYWORDDETECTOR**](ksnodetype-audio-keyworddetector.md)

[**KSNODETYPE\_コーラス**](ksnodetype-chorus.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_遅延**](ksnodetype-delay.md)

[**KSNODETYPE\_DEMUX**](ksnodetype-demux.md)

[**KSNODETYPE\_DEV\_特定**](ksnodetype-dev-specific.md)

[**KSNODETYPE\_DMSYNTH**](ksnodetype-dmsynth.md)

[**KSNODETYPE\_DMSYNTH\_キャップ**](ksnodetype-dmsynth-caps.md)

[**KSNODETYPE\_DRM\_DESCRAMBLE**](ksnodetype-drm-descramble.md)

[**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)

[**KSNODETYPE\_FM\_RX**](ksnodetype-fm-rx.md)

[**KSNODETYPE\_ラウドネス**](ksnodetype-loudness.md)

[**KSNODETYPE\_マイク\_配列\_プロセッサ**](ksnodetype-microphone-array-processor.md)

[**KSNODETYPE\_ミュート**](ksnodetype-mute.md)

[**KSNODETYPE\_MUX**](ksnodetype-mux.md)

[**KSNODETYPE\_ノイズ\_を抑制します。**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)

[**KSNODETYPE\_PROLOGIC\_エンコーダー**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE\_リバーブ**](ksnodetype-reverb.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODETYPE\_ステレオ\_の効果を高める**](ksnodetype-stereo-enhance.md)

[**KSNODETYPE\_ステレオ\_ワイド**](ksnodetype-stereo-wide.md)

[**KSNODETYPE\_合計**](ksnodetype-sum.md)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

[**KSNODETYPE\_SWMIDI**](ksnodetype-swmidi.md)

[**KSNODETYPE\_SWSYNTH**](ksnodetype-swsynth.md)

[**KSNODETYPE\_シンセサイザー**](ksnodetype-synthesizer.md)

[**KSNODETYPE\_テレフォニー\_双方向**](ksnodetype-telephony-bidi.md)

[**KSNODETYPE\_トーン**](ksnodetype-tone.md)

[**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)

 

 





