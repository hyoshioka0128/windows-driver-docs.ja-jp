---
title: KSPROPSETID\_オーディオ
description: KSPROPSETID\_オーディオ
ms.assetid: b65620c1-0460-430d-999d-f46fe0a2702d
keywords:
- KSPROPSETID_Audio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd44c7ca62cb07b866399ae3a7f438e923ce7830
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537618"
---
# <a name="kspropsetidaudio"></a>KSPROPSETID\_オーディオ


## <span id="ddk_kspropsetid_audio_ks"></span><span id="DDK_KSPROPSETID_AUDIO_KS"></span>


`KSPROPSETID_Audio`プロパティ セットは、データとオーディオのストリームでサポートされているコントロールの範囲を示します。 ミニポート ドライバーは、KSPROPERTY をサポートする必要があります\_オーディオ\_待機時間のプロパティ。 このプロパティ セット内の他のすべてのプロパティは省略可能です。

ハードウェアが機能をサポートしない場合、ミニポート ドライバーは、上位層のドライバーは、呼び出しを処理できるように、get および set プロパティの呼び出しのエラーを返す必要があります。 たとえば、ボリューム コントロールをサポートしていないハードウェアのミニポート ドライバーがエラーを返す必要があります、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](ksproperty-audio-volumelevel.md)呼び出しを有効にするため、ドライバー (カーネル ミキサー) などの履歴の上位にストリームのボリュームを設定します。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_オーディオ列挙値。

次のプロパティの一部である、`KSPROPSETID_Audio`プロパティ セット。

[**KSPROPERTY\_オーディオ\_3D\_インターフェイス**](ksproperty-audio-3d-interface.md)

[**KSPROPERTY\_オーディオ\_AGC**](ksproperty-audio-agc.md)

[**KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_オーディオ\_低音**](ksproperty-audio-bass.md)

[**KSPROPERTY\_オーディオ\_低音\_BOOST**](ksproperty-audio-bass-boost.md)

[**KSPROPERTY\_オーディオ\_バッファー\_期間**](ksproperty-audio-buffer-duration.md)

[**KSPROPERTY\_オーディオ\_チャネル\_構成**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_オーディオ\_コーラス\_レベル**](ksproperty-audio-chorus-level.md)

[**KSPROPERTY\_オーディオ\_コーラス\_変調\_深さ**](ksproperty-audio-chorus-modulation-depth.md)

[**KSPROPERTY\_オーディオ\_コーラス\_変調\_率**](ksproperty-audio-chorus-modulation-rate.md)

[**KSPROPERTY\_AUDIO\_COPY\_PROTECTION**](ksproperty-audio-copy-protection.md)

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_オーディオ\_遅延**](ksproperty-audio-delay.md)

[**KSPROPERTY\_AUDIO\_DEMUX\_DEST**](ksproperty-audio-demux-dest.md)

[**KSPROPERTY\_オーディオ\_DEV\_特定**](ksproperty-audio-dev-specific.md)

[**KSPROPERTY\_オーディオ\_動的\_範囲**](ksproperty-audio-dynamic-range.md)

[**KSPROPERTY\_オーディオ\_動的\_サンプリング\_率**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

[**KSPROPERTY\_AUDIO\_FILTER\_STATE**](ksproperty-audio-filter-state.md)

[**KSPROPERTY\_オーディオ\_待機時間**](ksproperty-audio-latency.md)

[**KSPROPERTY\_オーディオ\_線形\_バッファー\_位置**](ksproperty-audio-linear-buffer-position.md)

[**KSPROPERTY\_オーディオ\_ラウドネス**](ksproperty-audio-loudness.md)

[**KSPROPERTY\_オーディオ\_製造\_GUID**](ksproperty-audio-manufacture-guid.md)

[**KSPROPERTY\_AUDIO\_MIC\_ARRAY\_GEOMETRY**](ksproperty-audio-mic-array-geometry.md)

[**KSPROPERTY\_オーディオ\_MIC\_と小文字の区別**](ksproperty-audio-mic-sensitivity.md)

[**KSPROPERTY\_AUDIO\_MIC\_SNR**](ksproperty-audio-mic-snr.md)

[**KSPROPERTY\_オーディオ\_MID**](ksproperty-audio-mid.md)

[**KSPROPERTY\_オーディオ\_混在\_レベル\_キャップ**](ksproperty-audio-mix-level-caps.md)

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY\_オーディオ\_ミュート**](ksproperty-audio-mute.md)

[**KSPROPERTY\_AUDIO\_MUX\_SOURCE**](ksproperty-audio-mux-source.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER2**](ksproperty-audio-peakmeter2.md)

[**KSPROPERTY\_オーディオ\_位置**](ksproperty-audio-position.md)

[**KSPROPERTY\_オーディオ\_POSITIONEX**](ksproperty-audio-positionex.md)

[**KSPROPERTY\_オーディオ\_優先\_状態**](ksproperty-audio-preferred-status.md)

[**KSPROPERTY\_オーディオ\_プレゼンテーション\_位置**](ksproperty-audio-presentation-position.md)

[**KSPROPERTY\_オーディオ\_製品\_GUID**](ksproperty-audio-product-guid.md)

[**KSPROPERTY\_オーディオ\_品質**](ksproperty-audio-quality.md)

[**KSPROPERTY\_オーディオ\_リバーブ\_レベル**](ksproperty-audio-reverb-level.md)

[**KSPROPERTY\_オーディオ\_リバーブ\_時間**](ksproperty-audio-reverb-time.md)

[**KSPROPERTY\_オーディオ\_サンプリング\_率**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY\_オーディオ\_ステレオ\_の効果を高める**](ksproperty-audio-stereo-enhance.md)

[**KSPROPERTY\_AUDIO\_STEREO\_SPEAKER\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY\_オーディオ\_サラウンド\_エンコード**](ksproperty-audio-surround-encode.md)

[**KSPROPERTY\_AUDIO\_TREBLE**](ksproperty-audio-treble.md)

[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

[**KSPROPERTY\_オーディオ\_VOLUMELIMIT\_関心度の高い**](ksproperty-audio-volumelimit-engaged.md)

[**KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置**](ksproperty-audio-wavert-current-write-position.md)

[**KSPROPERTY\_AUDIO\_WAVERT\_CURRENT\_WRITE\_LASTBUFFER\_POSITION**](ksproperty-audio-wavert-current-write-lastbuffer-position.md)

[**KSPROPERTY\_オーディオ\_ワイド\_モード**](ksproperty-audio-wide-mode.md)

[**KSPROPERTY\_オーディオ\_ワイドかどうか**](ksproperty-audio-wideness.md)

 

 





