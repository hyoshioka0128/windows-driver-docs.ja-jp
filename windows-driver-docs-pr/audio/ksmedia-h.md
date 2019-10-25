---
title: Ksmedia.h
description: このセクションには、Ksmedia .h ヘッダーのリファレンストピックが含まれています。
ms.assetid: D5654BC1-45F5-4EC9-9E93-60318EF4C159
ms.date: 11/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 64832d3d9128df28a18a7f3a816a6ff6c7516491
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833093"
---
# <a name="ksmediah"></a>Ksmedia.h

このセクションには、Ksmedia .h ヘッダーのリファレンストピックが含まれています。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

|トピック|説明|
|--- |--- |
|[KSEVENT_CONTROL_CHANGE](ksevent-control-change.md)|KSEVENT_CONTROL_CHANGE イベントは、ハードウェアボリューム制御ノブ、ミュートスイッチ、またはその他の種類の手動コントロールを表すノードで、制御値の変更が発生したことを示します。 イベント値の種類 (操作データ) は、イベントに使用する通知の種類を指定する KSEVENTDATA 構造体です。|Pin|[KSE_NODE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)|[KSEVENTDATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)|
|[KSEVENT_LOOPEDSTREAMING_POSITION](ksevent-loopedstreaming-position.md)|KSEVENT_LOOPEDSTREAMING_POSITION イベントは、オーディオストリームがループバッファー内の指定された位置に達したことを示します。|
|[KSEVENT_SOUNDDETECTOR_MATCHDETECTED](ksevent-sounddetector-matchdetected.md)|KSEVENT_SOUNDDETECTOR_MATCHDETECTED イベントは、一致が検出されるたびに OS に通知するために、オーディオドライバーによって生成されます。|
|[KSJACK_DESCRIPTION](ksjack-description.md)|KSJACK_DESCRIPTION 構造体は、オーディオジャックの物理属性を指定します。|
|[KSJACK_DESCRIPTION2](ksjack-description2.md)|KSJACK_DESCRIPTION2 構造体は、ジャックのプレゼンス検出をサポートするジャックの機能と現在の状態を指定します。|
|[KSPROPERTY_AC3_ALTERNATE_AUDIO](ksproperty-ac3-alternate-audio.md)|KSPROPERTY_AC3_ALTERNATE_AUDIO プロパティは、AC 3 でエンコードされたストリームの2つの mono チャネルをステレオペアとして解釈するか、2つの独立したプログラムチャネルとして解釈するかを指定します。|
|[KSPROPERTY_AC3_BIT_STREAM_MODE](ksproperty-ac3-bit-stream-mode.md)|KSPROPERTY_AC3_BIT_STREAM_MODE プロパティは、AC-3 ストリームにエンコードされるオーディオサービスの種類であるビットストリームモードを指定します。|
|[KSPROPERTY_AC3_DIALOGUE_LEVEL](ksproperty-ac3-dialogue-level.md)|KSPROPERTY_AC3_DIALOGUE_LEVEL プロパティは、オーディオプログラム内で、AC 3 でエンコードされたストリームの平均音量レベルを指定します。|
|[KSPROPERTY_AC3_DOWNMIX](ksproperty-ac3-downmix.md)|KSPROPERTY_AC3_DOWNMIX プロパティは、スピーカーの構成に合わせて、AC 3 でエンコードされたストリームのプログラムチャネルを downmixed にする必要があるかどうかを指定します。|
|[KSPROPERTY_AC3_ERROR_CONCEALMENT](ksproperty-ac3-error-concealment.md)|KSPROPERTY_AC3_ERROR_CONCEALMENT プロパティは、再生中に AC 3 エンコードストリームのエラーを非隠れにする方法を指定します。|
|[KSPROPERTY_AC3_LANGUAGE_CODE](ksproperty-ac3-language-code.md)|KSPROPERTY_AC3_LANGUAGE_CODE プロパティは、AC 3 でエンコードされたストリームの言語コードを指定します。|
|[KSPROPERTY_AC3_ROOM_TYPE](ksproperty-ac3-room-type.md)|KSPROPERTY_AC3_ROOM_TYPE プロパティは、最終的なオーディオセッションが生成されたミックスルームの種類と調整を指定します。|
|[KSPROPERTY_AEC_MODE](ksproperty-aec-mode.md)|KSPROPERTY_AEC_MODE プロパティは、AEC ノードの操作モードを制御するために使用されます。 これは、AEC ノード ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) の省略可能なプロパティです。|
|[KSPROPERTY_AEC_NOISE_FILL_ENABLE](ksproperty-aec-noise-fill-enable.md)|KSPROPERTY_AEC_NOISE_FILL_ENABLE プロパティは、バックグラウンドノイズの塗りつぶしを有効または無効にするために使用されます。 これは、AEC ノード ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) の省略可能なプロパティです。|
|[KSPROPERTY_AEC_STATUS](ksproperty-aec-status.md)|KSPROPERTY_AEC_STATUS プロパティは、AEC ノード ([KSNODETYPE_ACOUSTIC_ECHO_CANCEL](ksnodetype-acoustic-echo-cancel.md)) の状態を監視するために使用されます。 これは、AEC ノードの省略可能なプロパティです。|
|[KSPROPERTY_AUDIO_3D_INTERFACE](ksproperty-audio-3d-interface.md)|KSPROPERTY_AUDIO_3D_INTERFACE プロパティは、サウンドバッファー内のデータを処理するために使用する3D アルゴリズムを指定します。|
|[KSPROPERTY_AUDIO_AGC](ksproperty-audio-agc.md)|KSPROPERTY_AUDIO_AGC プロパティは、AGC ノード ([KSNODETYPE_AGC](ksnodetype-agc.md)) のチャネルの agc (自動ゲイン制御) の状態を指定します。|
|[KSPROPERTY_AUDIO_ALGORITHM_INSTANCE](ksproperty-audio-algorithm-instance.md)|KSPROPERTY_AUDIO_ALGORITHM_INSTANCE プロパティは、ノードがオーディオデータストリームに適用するサードパーティの効果を実現するために使用される、デジタル信号処理 (DSP) アルゴリズムを指定します。 このプロパティに対して定義されている効果には、音響エコー取り消しやノイズ抑制などがあります。|
|[KSPROPERTY_AUDIO_BASS](ksproperty-audio-bass.md)|KSPROPERTY_AUDIO_BASS プロパティは、トーンノード ([KSNODETYPE_TONE](ksnodetype-tone.md)) のチャネルの低音レベルを指定します。|
|[KSPROPERTY_AUDIO_BASS_BOOST](ksproperty-audio-bass-boost.md)|KSPROPERTY_AUDIO_BASS_BOOST プロパティは、トーンノード ([KSNODETYPE_TONE](ksnodetype-tone.md)) のチャネルの低音ブーストを有効または無効にします。|
|[KSPROPERTY_AUDIO_BUFFER_DURATION](ksproperty-audio-buffer-duration.md)|KSPROPERTY_AUDIO_BUFFER_DURATION プロパティを使用すると、クライアントアプリケーションバッファーのサイズを期間として報告できます。|
|[KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)|KSPROPERTY_AUDIO_CHANNEL_CONFIG プロパティは、ノードが出力するオーディオストリーム内のチャネルの実際の空間位置を指定します。|
|[KSPROPERTY_AUDIO_CHORUS_LEVEL](ksproperty-audio-chorus-level.md)|KSPROPERTY_AUDIO_CHORUS_LEVEL プロパティは、コーラスレベルを指定します。 これは、コーラスノード ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH](ksproperty-audio-chorus-modulation-depth.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH プロパティは、コーラス変調の深さを指定します。 これは、コーラスノード ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE](ksproperty-audio-chorus-modulation-rate.md)|KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE プロパティは、コーラス変調率を指定します。 これは、コーラスノード ([KSNODETYPE_CHORUS](ksnodetype-chorus.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_COPY_PROTECTION](ksproperty-audio-copy-protection.md)|KSPROPERTY_AUDIO_COPY_PROTECTION プロパティは、オーディオストリームのコピー防止の状態を指定します。|
|[KSPROPERTY_AUDIO_CPU_RESOURCES](ksproperty-audio-cpu-resources.md)|KSPROPERTY_AUDIO_CPU_RESOURCES プロパティは、ノードの機能がハードウェアに実装されるか、またはホストの CPU で実行されるソフトウェアでエミュレートされるかを指定します。|
|[KSPROPERTY_AUDIO_DELAY](ksproperty-audio-delay.md)|KSPROPERTY_AUDIO_DELAY プロパティは、遅延ノード ([KSNODETYPE_DELAY](ksnodetype-delay.md)) が指定されたチャネルに導入するタイムラグを示します。|
|[KSPROPERTY_AUDIO_DEMUX_DEST](ksproperty-audio-demux-dest.md)|KSPROPERTY_AUDIO_DEMUX_DEST プロパティは、デマルチプレクサーが入力ストリームを送信する宛先ストリームを指定します。 これは、DEMUX ノード ([KSNODETYPE_DEMUX](ksnodetype-demux.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_DEV_SPECIFIC](ksproperty-audio-dev-specific.md)|KSPROPERTY_AUDIO_DEV_SPECIFIC プロパティは、デバイス固有のノード ([KSNODETYPE_DEV_SPECIFIC](ksnodetype-dev-specific.md)) のデバイス固有のプロパティにアクセスするために使用されます。|
|[KSPROPERTY_AUDIO_DYNAMIC_RANGE](ksproperty-audio-dynamic-range.md)|KSPROPERTY_AUDIO_DYNAMIC_RANGE プロパティは、ラウドネスノード ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md)) から出力されるオーディオストリームの動的範囲を指定します。|
|[KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE](ksproperty-audio-dynamic-sampling-rate.md)|KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE プロパティは、ノードのサンプリングレートの動的追跡を有効または無効にするために使用されます。|
|[KSPROPERTY_AUDIO_EQ_BANDS](ksproperty-audio-eq-bands.md)|KSPROPERTY_AUDIO_EQ_BANDS プロパティは、イコライゼーションテーブルからの周波数バンドのセットを指定します。 これは、EQ ノード ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) のチャネルの取得専用プロパティです。|
|[KSPROPERTY_AUDIO_EQ_LEVEL](ksproperty-audio-eq-level.md)|KSPROPERTY_AUDIO_EQ_LEVEL プロパティは、n 周波数バンドのエントリを含むイコライゼーションテーブルのイコライゼーションレベルを指定します。 これは、EQ ノード ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) のチャネルのプロパティです。|
|[KSPROPERTY_AUDIO_FILTER_STATE](ksproperty-audio-filter-state.md)|KSPROPERTY_AUDIO_FILTER_STATE プロパティは、サポートするプロパティセットの一覧について、GFX フィルターに対してクエリを実行するために使用されます。 リストは、プロパティセット Guid の配列の形式で取得されます。|
|[KSPROPERTY_AUDIO_LATENCY](ksproperty-audio-latency.md)|KSPROPERTY_AUDIO_LATENCY プロパティは、ストリームに関連付けられている遅延 (またはオーディオバッファリングの量) を報告するために使用されます。|
|[KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION](ksproperty-audio-linear-buffer-position.md)|KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION property 要求は、ストリームの開始以降に DMA がオーディオバッファーからフェッチしたバイト数を表す数値を取得します。|
|[KSPROPERTY_AUDIO_LOUDNESS](ksproperty-audio-loudness.md)|KSPROPERTY_AUDIO_LOUDNESS プロパティは、ラウドネスノード ([KSNODETYPE_LOUDNESS](ksnodetype-loudness.md)) のチャネルに対して、ラウドネス (全体的な動的範囲と低音ブースト) を有効または無効にするかどうかを指定します。|
|[KSPROPERTY_AUDIO_MANUFACTURE_GUID](ksproperty-audio-manufacture-guid.md)|このパラメーター名は将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY](ksproperty-audio-mic-array-geometry.md)|KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY プロパティは、マイク配列のジオメトリを指定します。|
|[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)|KSPROPERTY_AUDIO_MIC_SENSITIVITY プロパティは、フルスケール (dBFS) ユニットを基準としたマイクの感度をデシベル単位で指定します。|
|[KSPROPERTY_AUDIO_MIC_SNR](ksproperty-audio-mic-snr.md)|KSPROPERTY_AUDIO_MIC_SNR プロパティは、dB 単位でのマイク信号のノイズ比率 (SNR) メジャーを指定します。|
|[KSPROPERTY_AUDIO_MID](ksproperty-audio-mid.md)|KSPROPERTY_AUDIO_MID プロパティは、トーンノード ([KSNODETYPE_TONE](ksnodetype-tone.md)) 内のチャネルの中間周波数レベルを指定します。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_CAPS](ksproperty-audio-mix-level-caps.md)|KSPROPERTY_AUDIO_MIX_LEVEL_CAPS プロパティは、スーパーミキサーノード ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md)) の混合レベル機能を指定します。 1つの get プロパティ要求は、入力チャネルと出力チャネルのすべての組み合わせに関する情報を取得します。|
|[KSPROPERTY_AUDIO_MIX_LEVEL_TABLE](ksproperty-audio-mix-level-table.md)|KSPROPERTY_AUDIO_MIX_LEVEL_TABLE プロパティは、supermixer ノード ([KSNODETYPE_SUPERMIX](ksnodetype-supermix.md)) のミックスレベルを指定します。 すべての入力チャネルと出力チャネルに関する情報を提供します。|
|[KSPROPERTY_AUDIO_MUTE](ksproperty-audio-mute.md)|KSPROPERTY_AUDIO_MUTE プロパティは、ミュートノード ([KSNODETYPE_MUTE](ksnodetype-mute.md)) のチャネルがミュートされているかどうかを指定します。|
|[KSPROPERTY_AUDIO_MUX_SOURCE](ksproperty-audio-mux-source.md)|KSPROPERTY_AUDIO_MUX_SOURCE プロパティは、マルチプレクサーの出力ストリームのソースを指定します。 これは、MUX ノード ([KSNODETYPE_MUX](ksnodetype-mux.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_NUM_EQ_BANDS](ksproperty-audio-num-eq-bands.md)|KSPROPERTY_AUDIO_NUM_EQ_BANDS プロパティは、イコライゼーションテーブルの周波数バンドの数を取得するために使用されます。 これは、EQ ノード ([KSNODETYPE_EQUALIZER](ksnodetype-equalizer.md)) のチャネルの取得専用プロパティです。|
|[KSPROPERTY_AUDIO_PEAKMETER](ksproperty-audio-peakmeter.md)|KSPROPERTY_AUDIO_PEAKMETER プロパティは、peakmeter ノードが最後にリセットされたときから peakmeter ノード ([KSNODETYPE_PEAKMETER](ksnodetype-peakmeter.md)) で発生した最大オーディオ信号レベルを取得します。|
|[KSPROPERTY_AUDIO_PEAKMETER2](ksproperty-audio-peakmeter2.md)|Windows 8 では、peakmeter ノードが最後にリセットされてから peakmeter ノード (KSNODETYPE_PEAKMETER) で発生した最大オーディオ信号レベルを報告する KSPROPERTY_AUDIO_PEAKMETER2 プロパティが導入されています。|
|[KSPROPERTY_AUDIO_POSITION](ksproperty-audio-position.md)|KSPROPERTY_AUDIO_POSITION プロパティは、ピンのオーディオストリームのサウンドバッファー内の再生カーソルと書き込みカーソルの現在の位置を指定します。|
|[KSPROPERTY_AUDIO_POSITIONEX](ksproperty-audio-positionex.md)|KSPROPERTY_AUDIO_POSITIONEX プロパティは、ストリームの位置と、カーネルストリーミング (KS) ベースのオーディオドライバーに関連付けられたタイムスタンプ情報を呼び出し元に提供します。|
|[KSPROPERTY_AUDIO_PREFERRED_STATUS](ksproperty-audio-preferred-status.md)|KSPROPERTY_AUDIO_PREFERRED_STATUS プロパティは、デバイスがシステムの優先オーディオデバイスであることをデバイスに通知します。|
|[KSPROPERTY_AUDIO_PRESENTATION_POSITION](ksproperty-audio-presentation-position.md)|KSPROPERTY_AUDIO_PRESENTATION_POSITION property 要求は、エンドポイントにレンダリングされるオーディオデータ内の現在の位置を指定する構造体を取得します。|
|[KSPROPERTY_AUDIO_PRODUCT_GUID](ksproperty-audio-product-guid.md)|このパラメーター名は将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_QUALITY](ksproperty-audio-quality.md)|KSPROPERTY_AUDIO_QUALITY プロパティは、ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノード ([KSNODETYPE_SRC](ksnodetype-src.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_REVERB_LEVEL](ksproperty-audio-reverb-level.md)|KSPROPERTY_AUDIO_REVERB_LEVEL プロパティは、現在のリバーブレベルを指定します。 これはリバーブノード ([KSNODETYPE_REVERB](ksnodetype-reverb.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_REVERB_TIME](ksproperty-audio-reverb-time.md)|KSPROPERTY_AUDIO_REVERB_TIME プロパティは、リバーブの時間を指定します。 これはリバーブノード ([KSNODETYPE_REVERB](ksnodetype-reverb.md)) のプロパティです。|
|[KSPROPERTY_AUDIO_SAMPLING_RATE](ksproperty-audio-sampling-rate.md)|KSPROPERTY_AUDIO_SAMPLING_RATE プロパティは、出力ストリームを生成するために、ノードが入力ストリームをサンプリングする速度を指定します。|
|[KSPROPERTY_AUDIO_STEREO_ENHANCE](ksproperty-audio-stereo-enhance.md)|このパラメーター名は将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY](ksproperty-audio-stereo-speaker-geometry.md)|KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY プロパティは、ハードウェアアクセラレータの3D オーディオの DirectSound スピーカー構成プロパティを実装するために、 [KSPROPERTY_AUDIO_CHANNEL_CONFIG](ksproperty-audio-channel-config.md)と組み合わせて使用されます。 これは、DAC ノード ([KSNODETYPE_DAC](ksnodetype-dac.md)) と3d ノード ([KSNODETYPE_3D_EFFECTS](ksnodetype-3d-effects.md)) のオプションのプロパティです。|
|[KSPROPERTY_AUDIO_SURROUND_ENCODE](ksproperty-audio-surround-encode.md)|KSPROPERTY_AUDIO_SURROUND_ENCODE プロパティは、フィルターのサラウンドエンコーダーが有効か無効かを指定します。 サラウンドエンコーダーノード ([KSNODETYPE_PROLOGIC_ENCODER](ksnodetype-prologic-encoder.md)) は、Dolby サラウンド Pro ロジックエンコードを実行します。|
|[KSPROPERTY_AUDIO_TREBLE](ksproperty-audio-treble.md)|KSPROPERTY_AUDIO_TREBLE プロパティは、トーンノード ([KSNODETYPE_TONE](ksnodetype-tone.md)) のチャネルの高音レベルを指定します。|
|[KSPROPERTY_AUDIO_VOLUMELEVEL](ksproperty-audio-volumelevel.md)|KSPROPERTY_AUDIO_VOLUMELEVEL プロパティは、ボリュームノード ([KSNODETYPE_VOLUME](ksnodetype-volume.md)) 内のチャネルのボリュームレベルを指定します。|
|[KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED](ksproperty-audio-volumelimit-engaged.md)|KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED は、Windows 8.1 で設定された KSPROPSETID_Audio プロパティに追加された新しい KS プロパティです。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION](ksproperty-audio-wavert-current-write-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION property 要求では、WaveRT バッファーの現在の書き込み位置 (バイト単位) を指定します。 オフロードドライバーでは、この書き込み位置情報を使用して、WaveRT バッファーに含まれる有効なデータの量を知ることができます。|
|[KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION](ksproperty-audio-wavert-current-write-lastbuffer-position.md)|KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION プロパティは、オーディオバッファー内の最後の有効なバイトを示すために使用されます。|
|[KSPROPERTY_AUDIO_WIDE_MODE](ksproperty-audio-wide-mode.md)|このパラメーター名は将来使用するために予約されています。|
|[KSPROPERTY_AUDIO_WIDENESS](ksproperty-audio-wideness.md)|KSPROPERTY_AUDIO_WIDENESS プロパティは、ステレオイメージの WIDENESS (見かけ上の幅) を指定します。|
|[KSPROPERTY_AUDIOENGINE](ksproperty-audioengine.md)|[KSPROPSETID_AudioEngine](kspropsetid-audioengine.md)プロパティセットに含まれるプロパティは、この列挙によって定義され、 [KSNODETYPE_AUDIO_ENGINE](ksnodetype-audio-engine.md)ノードでサポートされている必要があります。|
|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)|[KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE](ksproperty-audioengine-buffer-size-limits.md)プロパティは、特定のデータ形式に対してハードウェアオーディオエンジンがサポートできるバッファーの最小サイズと最大サイズを示します。これは、インスタンスが呼び出されたときに指定されます。 バッファーサイズはバイト単位で指定します。|
|[KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)|オフロード対応のハードウェアソリューションのオーディオドライバーは、 [KSPROPERTY_AUDIOENGINE_DESCRIPTOR](ksproperty-audioengine-descriptor.md)を使用して、ハードウェアオーディオエンジンを表すノードに関する情報を提供します。|
|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md)|[KSPROPERTY_AUDIOENGINE_DEVICEFORMAT](ksproperty-audioengine-deviceformat.md) property 要求は、デバイス形式の設定に関して、オーディオエンジンノードの状態を取得または変更します。|
|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md)|[KSPROPERTY_AUDIOENGINE_GFXENABLE](ksproperty-audioengine-gfx-enable.md) property 要求を使用すると、オーディオドライバーは、グローバル効果処理機能に関して、オーディオエンジンノードの状態を取得または変更できます。|
|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md)|[KSPROPERTY_AUDIOENGINE_LFXENABLE](ksproperty-audioengine-lfx-enable.md) property 要求は、ローカル効果処理機能に関して、オーディオエンジンノードの状態を取得または変更します。|
|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md)|[KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION](ksproperty-audioengine-loopback-protection.md) property 要求を使用すると、オーディオドライバーはオーディオエンジンノードのループバック保護ステータスを設定できます。|
|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md)|[KSPROPERTY_AUDIOENGINE_MIXFORMAT](ksproperty-audioengine-mixformat.md) property 要求は、ハードウェアオーディオエンジンのミキサーの設定を取得します。|
|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md)|[KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS](ksproperty-audioengine-supporteddeviceformats.md) property 要求は、ハードウェアオーディオエンジンによってサポートされているデバイス形式を取得します。|
|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)|[KSPROPERTY_AUDIOENGINE_VOLUMELEVEL](ksproperty-audioengine-volumelevel.md)プロパティは、指定されたストリームのチャネルのボリュームレベルを指定します。|
|[KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID](ksproperty-audiogfx-capturetargetdeviceid.md)|KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID プロパティは、キャプチャストリームのソースであるオーディオデバイスのプラグアンドプレイデバイス ID を GFX フィルターに通知するために使用されます。|
|[KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID](ksproperty-audiogfx-rendertargetdeviceid.md)|KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID プロパティは、最終的なオーディオミックスをレンダリングするオーディオデバイスのプラグアンドプレイデバイス ID を GFX フィルターに通知するために使用されます。|
|[KSPROPERTY_AUDIOMODULE](ksproperty-audiomodule.md)|KSPROPERTY_AUDIOMODULE 列挙体は、取引先が定義したオーディオモジュールに関する情報を通信するためにオーディオドライバーによって使用される定数を定義します。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING](ksproperty-audiosignalprocessing.md)|KSPROPERTY_AUDIOSIGNALPROCESSING 列挙体は、オーディオドライバーがピンのオーディオ処理モードと接続するときに使用する定数を定義します。|
|[KSPROPERTY_AUDIOSIGNALPROCESSING_MODES](ksproperty-audiosignalprocessing-modes.md)|KSPROPERTY_AUDIOSIGNALPROCESSING_MODES プロパティは、ピンファクトリによってサポートされるオーディオシグナル処理モードの一覧を返します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_ALL](ksproperty-directsound3dbuffer-all.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_ALL プロパティは、指定されたバッファーのすべての DirectSound 3D バッファープロパティを取得または設定するために使用されます。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES](ksproperty-directsound3dbuffer-coneangles.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES プロパティは、3D サウンドバッファーのサウンドプロジェクションコーンの内側と外側の円錐の角度を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION](ksproperty-directsound3dbuffer-coneorientation.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEORIENTATION プロパティは、3D サウンドバッファーのサウンドプロジェクションコーンの向きを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME](ksproperty-directsound3dbuffer-coneoutsidevolume.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME プロパティは、3D サウンドバッファーのコーン外部サウンドボリュームを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE](ksproperty-directsound3dbuffer-maxdistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MAXDISTANCE プロパティは、3D サウンドバッファーの最大距離を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE](ksproperty-directsound3dbuffer-mindistance.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE プロパティは、3D サウンドバッファーの最小距離を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_MODE](ksproperty-directsound3dbuffer-mode.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_MODE プロパティは、3D サウンドバッファーの処理モードを指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION](ksproperty-directsound3dbuffer-position.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION プロパティは、3D サウンドバッファーの位置を指定します。|
|[KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY](ksproperty-directsound3dbuffer-velocity.md)|KSPROPERTY_DIRECTSOUND3DBUFFER_VELOCITY プロパティは、3D サウンドバッファーの速度を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALL](ksproperty-directsound3dlistener-all.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALL プロパティは、指定されたリスナー ID のすべての DirectSound 3D リスナープロパティを設定または取得するために使用されます。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION](ksproperty-directsound3dlistener-allocation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION プロパティは、リスナーデータ用の記憶域を割り当てて解放するタイミングをドライバーに通知するために使用されます。 ストレージは、リスナーの作成時に割り当てられ、リスナーが削除されると解放されます。 このプロパティは、リスナーデータが現在割り当てられているかどうかをドライバーに照会するためにも使用できます。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH](ksproperty-directsound3dlistener-batch.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH プロパティは、3D リスナーのバッチモード設定を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR](ksproperty-directsound3dlistener-distancefactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR プロパティは、距離の値に適用する距離係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR](ksproperty-directsound3dlistener-dopplerfactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR プロパティは、3D リスナーのドップラー係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION](ksproperty-directsound3dlistener-orientation.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION プロパティは、3D リスナーの向きを指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION](ksproperty-directsound3dlistener-position.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION プロパティは、3D リスナーの位置を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR](ksproperty-directsound3dlistener-rollofffactor.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR プロパティは、3D リスナーのロールオフ係数を指定します。|
|[KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY](ksproperty-directsound3dlistener-velocity.md)|KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY プロパティは、3D リスナーのベロシティベクターを指定します。|
|[KSPROPERTY_FMRX_ANTENNAENDPOINTID](ksproperty-fmrx-antennaendpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)プロパティには、FM アンテナとして使用されるエンドポイントに関する情報が含まれています。|
|[KSPROPERTY_FMRX_ENDPOINTID](ksproperty-fmrx-endpointid.md)|[KSTOPOLOGY_ENDPOINTID](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)プロパティには、FM ラジオの出力/レンダーエンドポイントのエンドポイント ID が含まれています。|
|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)|[KSPROPERTY_FMRX_VOLUME](ksproperty-fmrx-volume.md)プロパティは、FM ラジオの音量を制御します。|
|[KSPROPERTY_HRTF3D_FILTER_FORMAT](ksproperty-hrtf3d-filter-format.md)|KSPROPERTY_HRTF3D_FILTER_FORMAT プロパティは、HRTF アルゴリズムによって使用されるフィルター形式を取得します。|
|[KSPROPERTY_HRTF3D_INITIALIZE](ksproperty-hrtf3d-initialize.md)|KSPROPERTY_HRTF3D_INITIALIZE プロパティは、HRTF アルゴリズムの初期化に使用するパラメーター値を指定します。|
|[KSPROPERTY_HRTF3D_PARAMS](ksproperty-hrtf3d-params.md)|KSPROPERTY_HRTF3D_PARAMS プロパティは、HRTF アルゴリズムに3-d パラメーター値のセットを適用します。|
|[KSPROPERTY_ITD3D_PARAMS](ksproperty-itd3d-params.md)|KSPROPERTY_ITD3D_PARAMS プロパティは、3D ノードの ITD アルゴリズムによって使用されるパラメーターを設定するために使用されます。|
|[KSPROPERTY_JACK](ksproperty-jack.md)|KSPROPERTY_JACK 列挙体は、オーディオジャック構造体によって使用される新しいプロパティ Id を定義します。|
|[KSPROPERTY_JACK_CONTAINERID](ksproperty-jack-containerid.md)|KSPROPERTY_JACK_CONTAINERID プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。|
|[KSPROPERTY_JACK_DESCRIPTION](ksproperty-jack-description.md)|KSPROPERTY_JACK_DESCRIPTION プロパティは、フィルターハンドルを介してアクセスされる複数項目のピンごとのプロパティとして実装されます。|
|[KSPROPERTY_JACK_DESCRIPTION2](ksproperty-jack-description2.md)|KSPROPERTY_JACK_DESCRIPTION2 プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。|
|[KSPROPERTY_JACK_SINK_INFO](ksproperty-jack-sink-info.md)|KSPROPERTY_JACK_SINK_INFO プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。|
|[KSPROPERTY_ONESHOT_DISCONNECT](ksproperty-oneshot-disconnect.md)|KSPROPERTY_ONESHOT_DISCONNECT プロパティは、オーディオドライバーが Bluetooth オーディオデバイスとの接続を切断するように要求するために使用されます。|
|[KSPROPERTY_ONESHOT_RECONNECT](ksproperty-oneshot-reconnect.md)|KSPROPERTY_ONESHOT_RECONNECT プロパティは、Bluetooth オーディオデバイスへの接続を試行するようにオーディオドライバーに要求するために使用されます。|
|[KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)|KSPROPERTY_RTAUDIO_BUFFER プロパティは、オーディオデータ用にドライバーによって割り当てられる循環バッファーを指定します。|
|[KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)|KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION プロパティは、オーディオデータ用にドライバーによって割り当てられる循環バッファーを指定し、イベント通知要件を識別します。|
|[KSPROPERTY_RTAUDIO_CLOCKREGISTER](ksproperty-rtaudio-clockregister.md)|KSPROPERTY_RTAUDIO_CLOCKREGISTER プロパティは、オーディオデバイスのウォールクロックレジスタを、クライアントがアクセスできる仮想メモリの場所にマップします。|
|[KSPROPERTY_RTAUDIO_GETREADPACKET](ksproperty-rtaudio-getreadpacket.md)|KSPROPERTY_RTAUDIO_GETREADPACKET は、キャプチャされたオーディオパケットに関する情報を返します。|
|[KSPROPERTY_RTAUDIO_HWLATENCY](ksproperty-rtaudio-hwlatency.md)|KSPROPERTY_RTAUDIO_HWLATENCY プロパティは、オーディオハードウェアのストリーム待機時間とそれに関連付けられているデータパスの説明を取得します。|
|[KSPROPERTY_RTAUDIO_PACKETCOUNT](ksproperty-rtaudio-packetcount.md)|KSPROPERTY_RTAUDIO_PACKETCOUNT は、WaveRT バッファーからハードウェアに完全に転送されたパケットの数 (1 から始まる) を返します。|
|[KSPROPERTY_RTAUDIO_POSITIONREGISTER](ksproperty-rtaudio-positionregister.md)|KSPROPERTY_RTAUDIO_POSITIONREGISTER プロパティは、特定のストリームのオーディオデバイスの位置レジスタを、クライアントがアクセスできる仮想メモリ位置にマップします。|
|[KSPROPERTY_RTAUDIO_PRESENTATION_POSITION](ksproperty-rtaudio-presentation-position.md)|KSPROPERTY_RTAUDIO_PRESENTATION_POSITION はストリームプレゼンテーション情報を返します。|
|[KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT](ksproperty-rtaudio-query-notification-support.md)|クライアントアプリケーションは、KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT プロパティを使用して、送信されたバッファーで実行されたプロセスが完了したときに、オーディオドライバーがクライアントアプリケーションに通知できるかどうかを判断します。|
|[KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-register-notification-event.md)|KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT プロパティは、DMA ドリブンイベント通知のユーザーモードイベントを登録します。 [KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION](ksproperty-rtaudio-buffer-with-notification.md)を正常に呼び出した後、イベントを登録する必要があります。|
|[KSPROPERTY_RTAUDIO_SETWRITEPACKET](ksproperty-rtaudio-setwritepacket.md)|KSPROPERTY_RTAUDIO_SETWRITEPACKET は、OS が WaveRT バッファーに有効なデータを書き込んだことをドライバーに通知します。|
|[KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT](ksproperty-rtaudio-unregister-notification-event.md)|KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT プロパティは、DMA ドリブンイベント通知からユーザーモードイベントの登録を解除します。|
|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)|[KSPROPERTY_SOUNDDETECTOR](ksproperty-sounddetector.md)列挙体は、検出もサポートするオーディオキャプチャデバイスのフィルターを登録するために使用される定数を定義します。|
|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)|[KSPROPERTY_SOUNDDETECTOR_ARMED](ksproperty-sounddetector-armed.md)プロパティは、検出機能の現在の取り組ま状態です。|
|[KSPROPERTY_SOUNDDETECTOR_MATCHRESULT](ksproperty-sounddetector-matchresult.md)|KSPROPERTY_SOUNDDETECTOR_MATCHRESULT プロパティは、一致の結果データを保持します。|
|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)|[KSPROPERTY_SOUNDDETECTOR_PATTERNS](ksproperty-sounddetector-patterns.md)プロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。|
|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)|[KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md)プロパティは、サポートされているパターンの種類を識別する guid の一覧を取得するために使用されます。|
|[KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE](ksproperty-sysaudio-attach-virtual-source.md)|KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE プロパティは、仮想ソースを仮想オーディオデバイス上のピンインスタンスにアタッチします。|
|[KSPROPERTY_SYSAUDIO_COMPONENT_ID](ksproperty-sysaudio-component-id.md)|KSPROPERTY_SYSAUDIO_COMPONENT_ID プロパティは、指定された仮想オーディオデバイスが使用する wave レンダリングデバイスからコンポーネント ID を取得します。|
|[KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE](ksproperty-sysaudio-create-virtual-source.md)|KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE プロパティは、新しい仮想ソースを作成します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_COUNT](ksproperty-sysaudio-device-count.md)|KSPROPERTY_SYSAUDIO_DEVICE_COUNT プロパティは、DirectSound アプリケーションプログラムが選択する必要がある仮想オーディオデバイスの数を指定するカウントを取得します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME](ksproperty-sysaudio-device-friendly-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME プロパティは、仮想オーディオデバイスのフレンドリ名を含む Unicode 文字列を取得します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE](ksproperty-sysaudio-device-instance.md)|KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE プロパティは、仮想オーディオデバイスの現在のインスタンスを指定します。|
|[KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME](ksproperty-sysaudio-device-interface-name.md)|KSPROPERTY_SYSAUDIO_DEVICE_INTERFACE_NAME プロパティは、指定された仮想オーディオデバイスのプラグアンドプレイデバイスインターフェイス名を含む Unicode 文字列を取得します。|
|[KSPROPERTY_SYSAUDIO_INSTANCE_INFO](ksproperty-sysaudio-instance-info.md)|KSPROPERTY_SYSAUDIO_INSTANCE_INFO プロパティは、仮想オーディオデバイスを開き、そのデバイスの構成フラグを指定します。|
|[KSPROPERTY_SYSAUDIO_SELECT_GRAPH](ksproperty-sysaudio-select-graph.md)|KSPROPERTY_SYSAUDIO_SELECT_GRAPH プロパティは、仮想オーディオデバイス上のピンインスタンスに対して SysAudio がビルドする、オプションのノードをグラフに明示的に含めるために使用されます。|
|[KSPROPERTY_TELEPHONY_CALLCONTROL](ksproperty-telephony-callcontrol.md)|KSPROPERTY_TELEPHONY_CALLCONTROL プロパティは、通話を開始および終了するために使用されます。|
|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)|[KSPROPERTY_TELEPHONY_CALLHOLD](ksproperty-telephony-callhold.md)プロパティは、通話の保留状態を制御するために使用されます。|
|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)|[KSPROPERTY_TELEPHONY_CALLINFO](ksproperty-telephony-callinfo.md)プロパティは、呼び出しの状態や呼び出しの種類など、現在の呼び出し情報を取得するために使用されます。|
|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)|[KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR](ksproperty-telephony-endpointidpair.md)プロパティには、携帯電話のオーディオルーティング用のレンダーおよびキャプチャのエンドポイントが含まれています。|
|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)|[KSPROPERTY_TELEPHONY_MUTE_TX](ksproperty-telephony-mute-tx.md)プロパティは、ローカルマイクからリモートエンドに送信されるデータをミュートするかどうかを制御するために使用されます。|
|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)|[KSPROPERTY_TELEPHONY_PROVIDERCHANGE](ksproperty-telephony-providerchange.md)プロパティは、シングルラジオ音声通話の継続性 (srvcc) が開始または終了するオーディオドライバーと通信するために使用されます。|
|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)|[KSPROPERTY_TELEPHONY_PROVIDERID](ksproperty-telephony-providerid.md)プロパティは、プロバイダー識別子を wave フィルターに関連付けるためにオーディオドライバーによって使用されます。|
|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)|[KSPROPERTY_TELEPHONY_VOLUME](ksproperty-telephony-volume.md)プロパティは、すべての携帯電話用のボリュームを制御するために使用されます。|
|[KSPROPERTY_TOPOLOGYNODE_ENABLE](ksproperty-topologynode-enable.md)|KSPROPERTY_TOPOLOGYNODE_ENABLE プロパティは、既に構築されているトポロジでトポロジノードをオンまたはオフにするために使用します。|
|[KSPROPERTY_TOPOLOGYNODE_RESET](ksproperty-topologynode-reset.md)|KSPROPERTY_TOPOLOGYNODE_RESET プロパティは、ノードを完全にリセットし、初期状態に復元します。|
|[KSRTAUDIO_BUFFER_PROPERTY](ksrtaudio-buffer-property.md)|KSRTAUDIO_BUFFER_PROPERTY 構造体は、バッファーのベースアドレスと要求されたバッファーサイズを[Ksk プロパティ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体に追加します。 この構造体は、 [KSPROPERTY_RTAUDIO_BUFFER](ksproperty-rtaudio-buffer.md)を介したオーディオバッファーの割り当てを要求するためにクライアントによって使用されます。|


