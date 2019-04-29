---
title: Ksmedia.h
description: このセクションには、Ksmedia.h ヘッダーの参照トピックが含まれています。
ms.assetid: D5654BC1-45F5-4EC9-9E93-60318EF4C159
ms.date: 11/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 763afb3b4f28d1b66b8476f2d37ce193c0681cdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333423"
---
# <a name="ksmediah"></a>Ksmedia.h

このセクションには、Ksmedia.h ヘッダーの参照トピックが含まれています。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

|トピック|説明|
|--- |--- |
|[KSEVENT_CONTROL_CHANGE](ksevent-control-change.md)|KSEVENT_CONTROL_CHANGE イベントは、ハードウェア ボリューム コントロールのノブ、ミュート スイッチ、または手動のコントロールの他の種類を表すノードにあるコントロールの値の変更が発生したことを示します。 イベント値の型 (データの操作) は、イベントを使用する通知の種類を指定する KSEVENTDATA 構造です。|Pin|[KSE_NODE](https://msdn.microsoft.com/library/windows/hardware/ff561937)|[KSEVENTDATA](https://msdn.microsoft.com/library/windows/hardware/ff561750)|
|[KSEVENT_LOOPEDSTREAMING_POSITION](ksevent-loopedstreaming-position.md)|KSEVENT_LOOPEDSTREAMING_POSITION イベントは、オーディオのストリーム バッファーをループ内の指定位置に達したことを示します。|
|[KSEVENT_SOUNDDETECTOR_MATCHDETECTED](ksevent-sounddetector-matchdetected.md)|KSEVENT_SOUNDDETECTOR_MATCHDETECTED イベントは、一致が検出されたときに、OS に通知するオーディオ ドライバーによって生成されます。|
|[KSJACK_DESCRIPTION](ksjack-description.md)|KSJACK_DESCRIPTION 構造体には、オーディオ ジャックの物理属性を指定します。|
|[KSJACK_DESCRIPTION2](ksjack-description2.md)|KSJACK_DESCRIPTION2 構造体には、機能とサポートがプレゼンスの検出を jack jack の現在の状態を指定します。|
|[KSPROPERTY_AC3_ALTERNATE_AUDIO](ksproperty-ac3-alternate-audio.md)|KSPROPERTY_AC3_ALTERNATE_AUDIO プロパティは、ステレオのペアとして、または 2 つの独立したプログラム チャネルとして AC で 3 でエンコードされたストリームで 2 つの mono のチャネルを解釈するかどうかを指定します。|
|[KSPROPERTY_AC3_BIT_STREAM_MODE](ksproperty-ac3-bit-stream-mode.md)|KSPROPERTY_AC3_BIT_STREAM_MODE プロパティには、ビット ストリーム モードで、ac-3 ストリームにエンコードされたオーディオのサービスの種類を指定します。|
|[KSPROPERTY_AC3_DIALOGUE_LEVEL](ksproperty-ac3-dialogue-level.md)|KSPROPERTY_AC3_DIALOGUE_LEVEL プロパティは、AC で 3 でエンコードされたストリームにオーディオのプログラム内での会話の平均ボリューム レベルを指定します。|
|[KSPROPERTY_AC3_DOWNMIX](ksproperty-ac3-downmix.md)|KSPROPERTY_AC3_DOWNMIX プロパティは、AC で 3 でエンコードされたストリームでプログラムのチャネルがスピーカーの構成に合わせてミックス ダウンをする必要があるかどうかを指定します。|
|[KSPROPERTY_AC3_ERROR_CONCEALMENT](ksproperty-ac3-error-concealment.md)|KSPROPERTY_AC3_ERROR_CONCEALMENT プロパティには、再生中に非表示に AC で 3 でエンコードされたストリーム内エラーをする必要があります、方法を指定します。|
|[KSPROPERTY_AC3_LANGUAGE_CODE](ksproperty-ac3-language-code.md)|KSPROPERTY_AC3_LANGUAGE_CODE プロパティには、AC で 3 でエンコードされたストリームの言語コードを指定します。|
|[KSPROPERTY_AC3_ROOM_TYPE](ksproperty-ac3-room-type.md)|KSPROPERTY_AC3_ROOM_TYPE プロパティでは、最終的な音声セッションが生成された混合部屋の調整と型を指定します。|
|[KSPROPERTY_AEC_MODE](ksproperty-aec-mode.md)|KSPROPERTY_AEC_MODE プロパティは、操作の AEC ノードのモードの制御に使用されます。 これは省略可能な AEC ノードのプロパティ ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。|
|[KSPROPERTY_AEC_NOISE_FILL_ENABLE](ksproperty-aec-noise-fill-enable.md)|KSPROPERTY_AEC_NOISE_FILL_ENABLE プロパティは、有効にして、バック グラウンド ノイズの塗りつぶしを無効にするに使用されます。 これは省略可能な AEC ノードのプロパティ ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。|
|[KSPROPERTY_AEC_STATUS](ksproperty-aec-status.md)|AEC ノードの状態を監視する KSPROPERTY_AEC_STATUS プロパティが使用されます ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md))。 これは、AEC のノードのオプションのプロパティです。|
|[KSPROPERTY_AUDIO_3D_INTERFACE](ksproperty-audio-3d-interface.md)|KSPROPERTY_AUDIO_3D_INTERFACE プロパティには、3 D を使用してサウンド バッファー内のデータを処理するアルゴリズムを指定します。|
|[KSPROPERTY_AUDIO_AGC](ksproperty-audio-agc.md)|KSPROPERTY_AUDIO_AGC プロパティ AGC ノード内のチャネルの AGC (自動ゲイン制御) の状態を指定します ([KSNODETYPE_AGC](ksnodetype-agc.md))。|
|[KSPROPERTY_AUDIO_ALGORITHM_INSTANCE](ksproperty-audio-algorithm-instance.md)|KSPROPERTY_AUDIO_ALGORITHM_INSTANCE プロパティには、デジタル信号処理ノードがオーディオ データ ストリームに適用されるサード パーティ製の効果を実現するために使用される (DSP) アルゴリズムを指定します。 このプロパティに対して定義されている効果には、アコースティック エコー キャンセル機能とノイズの抑制が含まれます。|
|[KSPROPERTY_AUDIO_BASS](ksproperty-audio-bass.md)|KSPROPERTY_AUDIO_BASS プロパティ トーン ノードで、チャネルの低音レベルを指定します ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_BASS_BOOST](ksproperty-audio-bass-boost.md)|KSPROPERTY_AUDIO_BASS_BOOST プロパティができ、トーン ノードでのチャネルの音を無効にします ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_BUFFER_DURATION](ksproperty-audio-buffer-duration.md)|KSPROPERTY_AUDIO_BUFFER_DURATION プロパティでは、期間として報告されることをクライアント アプリケーションのバッファーのサイズを使用します。|
|[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)|KSPROPERTY_AUDIO_CHANNEL_CONFIG プロパティは、ノードを出力するオーディオ ストリーム内のチャネルの空間実際の配置を指定します。|
|[KSPROPERTY_AUDIO_CHORUS_LEVEL](ksproperty-audio-chorus-level.md)|KSPROPERTY_AUDIO_CHORUS_LEVEL プロパティには、コーラス レベルを指定します。 これはコーラス ノードのプロパティ ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH](ksproperty-audio-chorus-modulation-depth.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH プロパティには、コーラス変調深さを指定します。 これはコーラス ノードのプロパティ ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE](ksproperty-audio-chorus-modulation-rate.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE プロパティには、コーラス変調のレートを指定します。 これはコーラス ノードのプロパティ ([KSNODETYPE_CHORUS](ksnodetype-chorus.md))。|
|[KSPROPERTY_AUDIO_COPY_PROTECTION](ksproperty-audio-copy-protection.md)|KSPROPERTY_AUDIO_COPY_PROTECTION プロパティには、オーディオ ストリームのコピー防止の状態を指定します。|
|[KSPROPERTY_AUDIO_CPU_RESOURCES](ksproperty-audio-cpu-resources.md)|KSPROPERTY_AUDIO_CPU_RESOURCES プロパティは、ノードの機能がハードウェアでの実装や、ホストの CPU で実行されているソフトウェアがエミュレートされるかどうかを指定します。|
|[KSPROPERTY_AUDIO_DELAY](ksproperty-audio-delay.md)|KSPROPERTY_AUDIO_DELAY プロパティには、タイム ラグを示します。 その遅延ノード ([KSNODETYPE_DELAY](ksnodetype-delay.md)) は、指定したチャネルに導入します。|
|[KSPROPERTY_AUDIO_DEMUX_DEST](ksproperty-audio-demux-dest.md)|KSPROPERTY_AUDIO_DEMUX_DEST プロパティには、デマルチプレクサーがその入力ストリームを送信する先のストリームを指定します。 これは、プロパティは DEMUX ノードのプロパティ ([KSNODETYPE_DEMUX](ksnodetype-demux.md))。|
|[KSPROPERTY_AUDIO_DEV_SPECIFIC](ksproperty-audio-dev-specific.md)|デバイスに固有のノードでデバイスに固有のプロパティにアクセスする KSPROPERTY_AUDIO_DEV_SPECIFIC プロパティが使用されます ([KSNODETYPE_DEV_SPECIFIC](ksnodetype-dev-specific.md))。|
|[KSPROPERTY_AUDIO_DYNAMIC_RANGE](ksproperty-audio-dynamic-range.md)|KSPROPERTY_AUDIO_DYNAMIC_RANGE プロパティは、ラウドネスのノードから出力されるオーディオ ストリームの動的範囲を指定します ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md))。|
|[KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE](ksproperty-audio-dynamic-sampling-rate.md)|KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE プロパティは、有効にして、ノードのサンプリング レートの動的な追跡を無効にするに使用されます。|
|[KSPROPERTY_AUDIO_EQ_BANDS](ksproperty-audio-eq-bands.md)|KSPROPERTY_AUDIO_EQ_BANDS プロパティには、イコライゼーション テーブルからの周波数のバンドのセットを指定します。 これは EQ ノード内のチャネルの取得専用プロパティ ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_EQ_LEVEL](ksproperty-audio-eq-level.md)|KSPROPERTY_AUDIO_EQ_LEVEL プロパティには、n の頻度のバンドのエントリを含むイコライゼーション テーブル イコライゼーション レベルを指定します。 これは EQ ノード内のチャネルのプロパティ ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_FILTER_STATE](ksproperty-audio-filter-state.md)|KSPROPERTY_AUDIO_FILTER_STATE プロパティは、サポートされるプロパティ セットの一覧については、GFX フィルターのクエリに使用されます。 一覧は、プロパティ セット Guid の配列の形式で取得されます。|
|[KSPROPERTY_AUDIO_LATENCY](ksproperty-audio-latency.md)|遅延 (またはオーディオのバッファー量) をレポートに KSPROPERTY_AUDIO_LATENCY プロパティを使用したストリームに関連付けられています。|
|[KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION](ksproperty-audio-linear-buffer-position.md)|KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION プロパティ要求には、DMA をオーディオ バッファーからストリームの先頭からフェッチしたバイト数を表す数値を取得します。|
|[KSPROPERTY_AUDIO_LOUDNESS](ksproperty-audio-loudness.md)|KSPROPERTY_AUDIO_LOUDNESS プロパティは、ラウドネス (全体的なダイナミック レンジおよび音) が有効になっているまたはラウドネス ノードでのチャネルを無効になっているかどうかを指定します ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md))。|
|[KSPROPERTY_AUDIO_MANUFACTURE_GUID](ksproperty-audio-manufacture-guid.md)|このパラメーター名は、将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY](ksproperty-audio-mic-array-geometry.md)|KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY プロパティには、マイク配列のジオメトリを指定します。|
|[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)|KSPROPERTY_AUDIO_MIC_SENSITIVITY プロパティは、フル スケール (dBFS) ユニットの基準としたデシベル単位でマイクの感度を指定します。|
|[KSPROPERTY_AUDIO_MIC_SNR](ksproperty-audio-mic-snr.md)|KSPROPERTY_AUDIO_MIC_SNR プロパティは、dB ユニットで、マイクの信号にノイズの比率 (SNR) メジャーを指定します。|
|[KSPROPERTY_AUDIO_MID](ksproperty-audio-mid.md)|KSPROPERTY_AUDIO_MID プロパティ トーン ノードで、チャネルの頻度の中間レベルを指定します ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_CAPS](ksproperty-audio-mix-level-caps.md)|KSPROPERTY_AUDIO_MIX_LEVEL_CAPS プロパティ supermixer ノードのミックス レベル機能を指定します ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md))。 1 つのプロパティの get 要求では、入力と出力チャネルのすべての組み合わせの情報を取得します。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_TABLE](ksproperty-audio-mix-level-table.md)|KSPROPERTY_AUDIO_MIX_LEVEL_TABLE プロパティ supermixer ノードのミックス レベルを指定します ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md))。 すべての入力と出力チャネルの情報を提供します。|
|[KSPROPERTY_AUDIO_MUTE](ksproperty-audio-mute.md)|KSPROPERTY_AUDIO_MUTE プロパティを指定するかどうか、ミュート ノード上のチャネル ([KSNODETYPE_MUTE](ksnodetype-mute.md)) がミュートされているかどうか。|
|[KSPROPERTY_AUDIO_MUX_SOURCE](ksproperty-audio-mux-source.md)|KSPROPERTY_AUDIO_MUX_SOURCE プロパティには、マルチプレクサーの出力ストリームのソースを指定します。 これは、MUX ノードのプロパティ ([KSNODETYPE_MUX](ksnodetype-mux.md))。|
|[KSPROPERTY_AUDIO_NUM_EQ_BANDS](ksproperty-audio-num-eq-bands.md)|イコライゼーション テーブル内の周波数のバンドの数を取得する KSPROPERTY_AUDIO_NUM_EQ_BANDS プロパティが使用されます。 これは EQ ノード内のチャネルの取得専用プロパティ ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md))。|
|[KSPROPERTY_AUDIO_PEAKMETER](ksproperty-audio-peakmeter.md)|KSPROPERTY_AUDIO_PEAKMETER プロパティ peakmeter ノードで発生したオーディオ信号の最大レベルを取得します ([KSNODETYPE_PEAKMETER](ksnodetype-peakmeter.md)) peakmeter ノードの前回がリセットされました。|
|[KSPROPERTY_AUDIO_PEAKMETER2](ksproperty-audio-peakmeter2.md)|Windows 8 では、前回 peakmeter ノードがリセットされた後、peakmeter ノード (KSNODETYPE_PEAKMETER) で発生したオーディオ信号の最大レベルを報告する KSPROPERTY_AUDIO_PEAKMETER2 プロパティについて説明します。|
|[KSPROPERTY_AUDIO_POSITION](ksproperty-audio-position.md)|KSPROPERTY_AUDIO_POSITION プロパティは、ピンのオーディオ ストリームの音声バッファー内の再生、書き込みカーソルの現在の位置を指定します。|
|[KSPROPERTY_AUDIO_POSITIONEX](ksproperty-audio-positionex.md)|KSPROPERTY_AUDIO_POSITIONEX プロパティは、ストリームの位置と関連付けられているタイムスタンプ情報をストリーミング (KS) カーネルの呼び出し元のオーディオ ドライバーのベースします。|
|[KSPROPERTY_AUDIO_PREFERRED_STATUS](ksproperty-audio-preferred-status.md)|KSPROPERTY_AUDIO_PREFERRED_STATUS プロパティは、システムの優先するオーディオ デバイスであるデバイスを通知します。|
|[KSPROPERTY_AUDIO_PRESENTATION_POSITION](ksproperty-audio-presentation-position.md)|KSPROPERTY_AUDIO_PRESENTATION_POSITION プロパティ要求は、エンドポイントにレンダリングされるオーディオ データ内の現在位置を指定する構造体を取得します。|
|[KSPROPERTY_AUDIO_PRODUCT_GUID](ksproperty-audio-product-guid.md)|このパラメーター名は、将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_QUALITY](ksproperty-audio-quality.md)|KSPROPERTY_AUDIO_QUALITY プロパティには、ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノードのプロパティ ([KSNODETYPE_SRC](ksnodetype-src.md))。|
|[KSPROPERTY_AUDIO_REVERB_LEVEL](ksproperty-audio-reverb-level.md)|KSPROPERTY_AUDIO_REVERB_LEVEL プロパティには、現在のリバーブ レベルを指定します。 これはリバーブ ノードのプロパティ ([KSNODETYPE_REVERB](ksnodetype-reverb.md))。|
|[KSPROPERTY_AUDIO_REVERB_TIME](ksproperty-audio-reverb-time.md)|リバーブ KSPROPERTY_AUDIO_REVERB_TIME プロパティで指定します。 これはリバーブ ノードのプロパティ ([KSNODETYPE_REVERB](ksnodetype-reverb.md))。|
|[KSPROPERTY_AUDIO_SAMPLING_RATE](ksproperty-audio-sampling-rate.md)|KSPROPERTY_AUDIO_SAMPLING_RATE プロパティは、位置のノードは、出力ストリームを生成するために、入力ストリームをサンプル レートを指定します。|
|[KSPROPERTY_AUDIO_STEREO_ENHANCE](ksproperty-audio-stereo-enhance.md)|このパラメーター名は、将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY](ksproperty-audio-stereo-speaker-geometry.md)|組み合わせて KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY プロパティが使用される[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)ハードウェア アクセラレータを使用した 3D オーディオ DirectSound スピーカー構成プロパティを実装します。 これは省略可能な DAC のノードのプロパティ ([KSNODETYPE_DAC](ksnodetype-dac.md)) と 3D のノード ([KSNODETYPE_3D_EFFECTS](ksnodetype-3d-effects.md))。|
|[KSPROPERTY_AUDIO_SURROUND_ENCODE](ksproperty-audio-surround-encode.md)|KSPROPERTY_AUDIO_SURROUND_ENCODE プロパティは、フィルターのブロックの挿入のエンコーダーが有効になっているかどうかを指定します。 ブロックの挿入エンコーダー ノード ([KSNODETYPE_PROLOGIC_ENCODER](ksnodetype-prologic-encoder.md)) ドルビー サラウンド Pro ロジックのエンコードを実行します。|
|[KSPROPERTY_AUDIO_TREBLE](ksproperty-audio-treble.md)|KSPROPERTY_AUDIO_TREBLE プロパティ トーン ノードで、チャネルの音レベルを指定します ([KSNODETYPE_TONE](ksnodetype-tone.md))。|
|[KSPROPERTY_AUDIO_VOLUMELEVEL](ksproperty-audio-volumelevel.md)|KSPROPERTY_AUDIO_VOLUMELEVEL プロパティは、[ボリューム] ノードでチャネルのボリューム レベルを指定します ([KSNODETYPE_VOLUME](ksnodetype-volume.md))。|
|[KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED](ksproperty-audio-volumelimit-engaged.md)|KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED は、Windows 8.1 で設定 KSPROPSETID_Audio プロパティに追加されている新しい KS プロパティです。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION](ksproperty-audio-wavert-current-write-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION プロパティ要求では、現在では、WaveRT バッファーの位置を書き込む (バイト単位) を指定します。 オフロード ドライバーでは、WaveRT バッファーで有効なデータの量を把握するのにこの書き込み位置情報を使用できます。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION](ksproperty-audio-wavert-current-write-lastbuffer-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION プロパティは、オーディオのバッファー内の最後の有効なバイトを示すために使用されます。|
|[KSPROPERTY_AUDIO_WIDE_MODE](ksproperty-audio-wide-mode.md)|このパラメーター名は、将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_WIDENESS](ksproperty-audio-wideness.md)|KSPROPERTY_AUDIO_WIDENESS プロパティには、ステレオのイメージのワイドかどうか (明らかな幅) を指定します。|
|[KSPROPERTY_AUDIOENGINE](ksproperty-audioengine.md)|含まれるプロパティ、 [KSPROPSETID_AudioEngine](kspropsetid-audioengine.md)プロパティ セットは、この列挙体によって定義されでサポートする必要を[KSNODETYPE_AUDIO_ENGINE](ksnodetype-audio-engine.md)ノード。|
|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)プロパティが呼び出されると、インスタンスでの特定のデータ形式をサポートできるハードウェア オーディオ エンジン バッファーの最小値と最大サイズを示します。 バッファー サイズはバイト単位で指定します。|
|[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)|オフロード機能を備えたハードウェア ソリューションのオーディオ ドライバーを使用して[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)ハードウェア オーディオ エンジンを表すノードに関する情報を提供します。|
|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)プロパティ要求を取得または設定、デバイスの形式に関する、オーディオ エンジン ノードの状態を変更します。|
|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)プロパティ要求により、オーディオ ドライバーを取得またはそのグローバル効果の処理能力に関する、オーディオ エンジン ノードの状態を変更します。|
|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)プロパティ要求を取得または処理能力のローカルの効果に関して、オーディオ エンジン ノードの状態を変更します。|
|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)プロパティ要求により、オーディオ ドライバー、オーディオ エンジン ノードのループバック保護の状態を設定します。|
|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)プロパティ要求が、ハードウェアのオーディオ エンジンでミキサーの設定を取得します。|
|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)プロパティ要求が、ハードウェアのオーディオ エンジンでサポートされているデバイスの形式を取得します。|
|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)プロパティで指定したストリーム チャネルのボリューム レベルを指定します。|
|[KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID](ksproperty-audiogfx-capturetargetdeviceid.md)|KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID プロパティは、キャプチャ ストリームのソースであるオーディオ デバイスのプラグ アンド プレイ デバイス ID の GFX フィルターを通知するために使用されます。|
|[KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID](ksproperty-audiogfx-rendertargetdeviceid.md)|KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID プロパティは、最終的なオーディオ ミックスをレンダリングするオーディオ デバイスのプラグ アンド プレイ デバイス ID の GFX フィルターを通知するために使用されます。|
|[KSPROPERTY_AUDIOMODULE](ksproperty-audiomodule.md)|KSPROPERTY_AUDIOMODULE 列挙型では、通信パートナーに関する情報は、オーディオのモジュールを定義するために、オーディオ ドライバーによって使用される定数を定義します。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING](ksproperty-audiosignalprocessing.md)|KSPROPERTY_AUDIOSIGNALPROCESSING 列挙体は、オーディオ ドライバー関連ピンのオーディオの処理モードで使用される定数を定義します。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING_MODES](ksproperty-audiosignalprocessing-modes.md)|KSPROPERTY_AUDIOSIGNALPROCESSING_MODES プロパティは、pin factory でサポートされるオーディオ信号処理モードの一覧を返します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_ALL](ksproperty-directsound3dbuffer-all.md)|取得または指定したバッファーの DirectSound 3D バッファーのすべてのプロパティを設定する KSPROPERTY_DIRECTSOUND3DBUFFER_ALL プロパティが使用されます。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES](ksproperty-directsound3dbuffer-coneangles.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES プロパティは、内側と 3D のサウンド バッファーのプロジェクションのサウンド コーンの外側の円錐の角度を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION](ksproperty-directsound3dbuffer-coneorientation.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION プロパティでは、サウンド投影 3D サウンド バッファー円錐の向きを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME](ksproperty-directsound3dbuffer-coneoutsidevolume.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME プロパティには 3D サウンド バッファーの円錐外部サウンドのボリュームを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE](ksproperty-directsound3dbuffer-maxdistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE プロパティには 3D サウンド バッファーの最大距離を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE](ksproperty-directsound3dbuffer-mindistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE プロパティには 3D サウンド バッファーの最小距離を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MODE](ksproperty-directsound3dbuffer-mode.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MODE プロパティには 3D サウンド バッファーの処理モードを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION](ksproperty-directsound3dbuffer-position.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION プロパティには 3D サウンド バッファーの位置を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY](ksproperty-directsound3dbuffer-velocity.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY プロパティには 3D サウンド バッファーの速度を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALL](ksproperty-directsound3dlistener-all.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALL プロパティが設定または指定されたリスナー id DirectSound 3D リスナーのすべてのプロパティを取得するために使用します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION](ksproperty-directsound3dlistener-allocation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION プロパティは、ドライバーに指示を割り当て、そのリスナーのデータのストレージを解放する場合に使用されます。 リスナーが作成され、リスナーが削除されたときに解放されるときに、ストレージが割り当てられます。 このプロパティは、クエリでは、リスナーのデータが現在割り当てられているかどうかをドライバーにも使用できます。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH](ksproperty-directsound3dlistener-batch.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH プロパティには、3 D リスナーのバッチ モードの設定を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR](ksproperty-directsound3dlistener-distancefactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR プロパティには、距離の値に適用される距離係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR](ksproperty-directsound3dlistener-dopplerfactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR プロパティは、3 D リスナーのドップラー係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION](ksproperty-directsound3dlistener-orientation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION プロパティには、3 D リスナーの向きを指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION](ksproperty-directsound3dlistener-position.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION プロパティには、3 D リスナーの位置を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR](ksproperty-directsound3dlistener-rollofffactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR プロパティは、3 D リスナーのロールオフ係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY](ksproperty-directsound3dlistener-velocity.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY プロパティには、3 D リスナーの速度ベクターを指定します。|
|[KSPROPERTY_FMRX_ANTENNAENDPOINTID](ksproperty-fmrx-antennaendpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://msdn.microsoft.com/library/windows/hardware/mt169886)プロパティには、FM アンテナとして使用するエンドポイントに関する情報が含まれています。|
|[KSPROPERTY_FMRX_ENDPOINTID](ksproperty-fmrx-endpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://msdn.microsoft.com/library/windows/hardware/mt169886)プロパティには、FM ラジオ出力レンダー/エンドポイントのエンドポイント ID が含まれています。|
|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)プロパティは、FM ラジオの量を制御します。|
|[KSPROPERTY_HRTF3D_FILTER_FORMAT](ksproperty-hrtf3d-filter-format.md)|KSPROPERTY_HRTF3D_FILTER_FORMAT プロパティは、HRTF アルゴリズムで使用されるフィルターの形式を取得します。|
|[KSPROPERTY_HRTF3D_INITIALIZE](ksproperty-hrtf3d-initialize.md)|KSPROPERTY_HRTF3D_INITIALIZE プロパティには、HRTF アルゴリズムを初期化するために使用するパラメーター値を指定します。|
|[KSPROPERTY_HRTF3D_PARAMS](ksproperty-hrtf3d-params.md)|KSPROPERTY_HRTF3D_PARAMS プロパティには、HRTF アルゴリズムに一連の 3-D パラメーターの値が適用されます。|
|[KSPROPERTY_ITD3D_PARAMS](ksproperty-itd3d-params.md)|KSPROPERTY_ITD3D_PARAMS プロパティは、3 D のノードの ITD アルゴリズムによって使用されるパラメーターの設定に使用されます。|
|[KSPROPERTY_JACK](ksproperty-jack.md)|KSPROPERTY_JACK 列挙体は、新しいプロパティのオーディオ ジャック構造体によって使用されている Id を定義します。|
|[KSPROPERTY_JACK_CONTAINERID](ksproperty-jack-containerid.md)|KSPROPERTY_JACK_CONTAINERID プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。|
|[KSPROPERTY_JACK_DESCRIPTION](ksproperty-jack-description.md)|KSPROPERTY_JACK_DESCRIPTION プロパティは、フィルター ハンドル経由でアクセスする複数の項目、pin-wise プロパティとして実装されます。|
|[KSPROPERTY_JACK_DESCRIPTION2](ksproperty-jack-description2.md)|KSPROPERTY_JACK_DESCRIPTION2 プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。|
|[KSPROPERTY_JACK_SINK_INFO](ksproperty-jack-sink-info.md)|KSPROPERTY_JACK_SINK_INFO プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。|
|[KSPROPERTY_ONESHOT_DISCONNECT](ksproperty-oneshot-disconnect.md)|KSPROPERTY_ONESHOT_DISCONNECT プロパティは、Bluetooth のオーディオ デバイスから切断するオーディオ ドライバーの確認に使用されます。|
|[KSPROPERTY_ONESHOT_RECONNECT](ksproperty-oneshot-reconnect.md)|KSPROPERTY_ONESHOT_RECONNECT プロパティは、Bluetooth のオーディオ デバイスに接続しようとするオーディオ ドライバーの確認に使用されます。|
|[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)|KSPROPERTY_RTAUDIO_BUFFER プロパティには、ドライバーによって割り当てられた循環バッファーのオーディオ データを指定します。|
|[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)|KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION プロパティは、オーディオ データのドライバーに割り当てられた循環バッファーを指定し、イベント通知の要件を識別します。|
|[KSPROPERTY_RTAUDIO_CLOCKREGISTER](ksproperty-rtaudio-clockregister.md)|KSPROPERTY_RTAUDIO_CLOCKREGISTER プロパティは、オーディオ デバイスのウォール クロック レジスタをクライアントがアクセスできる仮想メモリの場所にマップします。|
|[KSPROPERTY_RTAUDIO_GETREADPACKET](ksproperty-rtaudio-getreadpacket.md)|KSPROPERTY_RTAUDIO_GETREADPACKET では、キャプチャされたオーディオ パケットに関する情報を返します。|
|[KSPROPERTY_RTAUDIO_HWLATENCY](ksproperty-rtaudio-hwlatency.md)|KSPROPERTY_RTAUDIO_HWLATENCY プロパティは、オーディオ ハードウェアとの関連付けられているデータ パスのストリームの待機時間の記述を取得します。|
|[KSPROPERTY_RTAUDIO_PACKETCOUNT](ksproperty-rtaudio-packetcount.md)|KSPROPERTY_RTAUDIO_PACKETCOUNT では、(1 から始まる) のハードウェアに WaveRT バッファーから完全に転送パケットの数を返します。|
|[KSPROPERTY_RTAUDIO_POSITIONREGISTER](ksproperty-rtaudio-positionregister.md)|KSPROPERTY_RTAUDIO_POSITIONREGISTER プロパティは、特定のストリームをオーディオ デバイスの位置の登録をクライアントがアクセスできる仮想メモリの場所にマップします。|
|[KSPROPERTY_RTAUDIO_PRESENTATION_POSITION](ksproperty-rtaudio-presentation-position.md)|KSPROPERTY_RTAUDIO_PRESENTATION_POSITION は、ストリーム プレゼンテーションの情報を返します。|
|[KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT](ksproperty-rtaudio-query-notification-support.md)|クライアント アプリケーションでは、KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT プロパティを使用して、かどうか、オーディオ ドライバーに通知できます、クライアント アプリケーションと、送信されたバッファーで実行されるプロセスが完了したかを判断します。|
|[KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-register-notification-event.md)|KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT プロパティは、DMA 駆動のイベント通知のユーザー モード イベントを登録します。 正常に呼び出した後のイベントを登録する必要があります[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)します。|
|[KSPROPERTY_RTAUDIO_SETWRITEPACKET](ksproperty-rtaudio-setwritepacket.md)|KSPROPERTY_RTAUDIO_SETWRITEPACKET は、OS に WaveRT バッファーに有効なデータによって書き込まれたことをドライバーに通知します。|
|[KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-unregister-notification-event.md)|KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT プロパティには、DMA 駆動のイベント通知からのユーザー モード イベントが登録解除します。|
|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)列挙体は、登録、検出機能をサポートするオーディオ キャプチャ デバイス用のフィルターに使用される定数を定義します。|
|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)プロパティは、検出機能の現在の arming 状態。|
|[KSPROPERTY_SOUNDDETECTOR_MATCHRESULT](ksproperty-sounddetector-matchresult.md)|KSPROPERTY_SOUNDDETECTOR_MATCHRESULT プロパティは、一致を結果のデータを保持します。|
|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)を検出するキーワードを構成するオペレーティング システムで設定されます。|
|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)プロパティがサポートされているパターンの種類を識別する Guid の一覧を取得するために使用します。|
|[KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE](ksproperty-sysaudio-attach-virtual-source.md)|KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE プロパティは、仮想のソースを仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスにアタッチします。|
|[KSPROPERTY_SYSAUDIO_COMPONENT_ID](ksproperty-sysaudio-component-id.md)|KSPROPERTY_SYSAUDIO_COMPONENT_ID プロパティは、指定した仮想のオーディオ デバイスで使用される wave レンダリング デバイスからのコンポーネントの ID を取得します。|
|[KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE](ksproperty-sysaudio-create-virtual-source.md)|KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE プロパティは、新しい仮想ソースを作成します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_COUNT](ksproperty-sysaudio-device-count.md)|KSPROPERTY_SYSAUDIO_DEVICE_COUNT プロパティは、DirectSound アプリケーション プログラムがから選択する必要があります仮想のオーディオ デバイスの数を指定する数を取得します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME](ksproperty-sysaudio-device-friendly-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME プロパティは、仮想のオーディオ デバイスのフレンドリ名を含む Unicode 文字列を取得します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE](ksproperty-sysaudio-device-instance.md)|KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE プロパティには、仮想のオーディオ デバイスの現在のインスタンスを指定します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME](ksproperty-sysaudio-device-interface-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME プロパティは、指定した仮想のオーディオ デバイスのプラグ アンド プレイ デバイス インターフェイス名を含む Unicode 文字列を取得します。|
|[KSPROPERTY_SYSAUDIO_INSTANCE_INFO](ksproperty-sysaudio-instance-info.md)|KSPROPERTY_SYSAUDIO_INSTANCE_INFO プロパティは、仮想のオーディオ デバイスを開き、そのデバイスの構成フラグを指定します。|
|[KSPROPERTY_SYSAUDIO_SELECT_GRAPH](ksproperty-sysaudio-select-graph.md)|SysAudio が仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスの構築をグラフに省略可能なノードを明示的に含める KSPROPERTY_SYSAUDIO_SELECT_GRAPH プロパティが使用されます。|
|[KSPROPERTY_TELEPHONY_CALLCONTROL](ksproperty-telephony-callcontrol.md)|KSPROPERTY_TELEPHONY_CALLCONTROL プロパティを起動し、電話の呼び出しを終了に使用されます。|
|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)通話の保留中の状態を制御するプロパティを使用します。|
|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)呼び出しの状態と呼び出しの種類など、現在の呼び出し情報を取得するプロパティを使用します。|
|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)プロパティに携帯電話の音声ルーティングのレンダリングとキャプチャのエンドポイントが含まれています。|
|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)リモートの末尾にローカルのマイクから送信されるデータをミュートするかどうかを制御するプロパティを使用します。|
|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)プロパティは、単一ラジオ音声通話の継続性 (SRVCC) が開始または終了するオーディオ ドライバーとの通信に使用します。|
|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)プロパティは、wave フィルター プロバイダーの識別子を関連付けるオーディオ ドライバーによって使用されます。|
|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)プロパティを使用して、携帯電話のすべての呼び出しの量を制御します。|
|[KSPROPERTY_TOPOLOGYNODE_ENABLE](ksproperty-topologynode-enable.md)|KSPROPERTY_TOPOLOGYNODE_ENABLE プロパティは、オンまたはオフ、既にビルドされたトポロジでのトポロジのノードに使用されます。|
|[KSPROPERTY_TOPOLOGYNODE_RESET](ksproperty-topologynode-reset.md)|KSPROPERTY_TOPOLOGYNODE_RESET プロパティをリセット ノード完全に初期状態に復元します。|
|[KSRTAUDIO_BUFFER_PROPERTY](ksrtaudio-buffer-property.md)|バッファーの基本アドレスを要求したバッファーのサイズを KSRTAUDIO_BUFFER_PROPERTY 構造体を追加します、 [KSPROPERTY](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 この構造を使用してオーディオ バッファーの割り当てを要求するクライアントによって使用される[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)します。|


