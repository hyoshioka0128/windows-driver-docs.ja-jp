---
title: オーディオ ドライバーの構造体
description: オーディオ ドライバーの構造体
ms.assetid: 8257342f-474a-42b3-809d-96fdeede398b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b1998f533b5b400f97ba50354a96d367411e12b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833815"
---
# <a name="audio-drivers-structures"></a>オーディオ ドライバーの構造体

## <span id="ddk_audio_drivers_structures_ks"></span><span id="DDK_AUDIO_DRIVERS_STRUCTURES_KS"></span>

ここでは、WDM オーディオミニポートドライバーによって使用される構造について説明します。 構造体の一覧は次のとおりです。

[**APO\_REG\_のプロパティ**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apo_reg_properties)

[**アポストロフィ Initbasestruct**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitbasestruct)

[**アポストロフィ (システム効果)** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects)

[**APOInitSystemEffects2**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-apoinitsystemeffects2)

[**AudioFXExtensionParams**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-audiofxextensionparams)

[**DMUS\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)

[**DRMFORWARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmforward)

[**DRMRIGHTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)

[**DS3DVECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ds3dvector)

[**KSAC3\_代替\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_alternate_audio)

[**KSAC3\_ビット\_ストリーム\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)

[**KSAC3\_ダイアログ\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_dialogue_level)

[**KSAC3\_DOWNMIX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_downmix)

[**KSAC3\_エラー\_CONCEALMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)

[**KSAC3\_言語\_コード**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537081(v=vs.85))

[**KSAC3\_ルーム\_種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_room_type)

[**KSAUDIO\_チャネル\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSAUDIO\_コピー\_保護**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)

[**KSAUDIO\_動的\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

[**KSAUDIO\_MIC\_配列\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSAUDIO\_マイクの\_座標**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_microphone_coordinates)

[**KSAUDIO\_ミックス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mix_caps)

[**KSAUDIO\_MIXCAP\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSAUDIO\_MIXLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSAUDIO\_PACKETSIZE\_の制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)

[**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

[**KSAUDIO\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)

[**KSAUDIO\_POSITIONEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSAUDIO\_優先\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)

[**KSAUDIO\_プレゼンテーション\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position)

[**KSAUDIOENGINE\_BUFFER\_SIZE\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSAUDIOENGINE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor)

[**KSAUDIOENGINE\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSK DATAR\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)

[**KSK DATAR\_ミュージック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)

[**KSDRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-ksdrmaudiostream_contentid)

[**KSDSOUND\_BUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdsound_bufferdesc)

[**KSDS3D\_バッファー\_すべて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)

[**KSDS3D\_バッファー\_円錐\_角度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

[**KSDS3D\_HRTF\_INIT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)

[**KSDS3D\_HRTF\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)

[**KSDS3D\_ITD\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params)

[**KSDS3D\_ITD\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params_msg)

[**KSDS3D\_リスナー\_すべて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)

[**KSDS3D\_リスナー\_の向き**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_orientation)

[**KSJACK\_の説明**](ksjack-description.md)

[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[**KSK ジャック\_シンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksjack_sink_information)

[**KSMUSICFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksmusicformat)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSP\_DRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-ksp_drmaudiostream_contentid)

[**KSP\_PINMODE**](https://docs.microsoft.com/windows/desktop/api/msapofxproxy/ns-msapofxproxy-tagksp_pinmode)

[KSRTAUDIO 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/index)

[**KSTELEPHONY\_CALLCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol)

[**KSTELEPHONY\_CALLINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)

[**KSTELEPHONY\_PROVIDERCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)

[**KSTOPOLOGY\_ENDPOINTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)

[**KSTOPOLOGY\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)

[**LOOPEDSTREAMING\_POSITION\_イベント\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

[**MDEVICECAPSEX**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-mdevicecapsex)

[**MIDIOPENDESC**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)

[**RTAUDIO\_GETREADPACKET\_情報**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt169891(v=vs.85))

[**RTAUDIO\_SETWRITEPACKET\_情報**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt169892(v=vs.85))

[**SOUNDDETECTOR\_PATTERN ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**シンセサイザー\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer)

[**シンセサイザー\_PORTPARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)

[**シンセサイザー\_の統計**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats)

[**SYNTHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)

[**SYNTHDOWNLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload)

[**SYNTHVOICEPRIORITY\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance)

[**SYSAUDIO\_\_仮想\_ソースにアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**SYSAUDIO\_\_仮想\_ソースの作成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**SYSAUDIO\_インスタンス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)

[**SYSAUDIO\_\_グラフの選択**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)

[**UNCOMPRESSEDAUDIOFORMAT**](https://docs.microsoft.com/windows/desktop/api/audiomediatype/ns-audiomediatype-uncompressedaudioformat)

[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)

[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)
