---
title: KSPROPERTY\_オーディオ\_チャネル\_構成
description: KSPROPERTY\_オーディオ\_チャネル\_構成プロパティは、ノードを出力するオーディオ ストリームでチャネルの空間実際の配置を指定します。
ms.assetid: 5ce9bf4a-c84e-4d7e-8e75-896c88ec1a72
keywords:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88f79c93576ee5f8dccfd4610e459919eb8b5587
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571566"
---
# <a name="kspropertyaudiochannelconfig"></a>KSPROPERTY\_オーディオ\_チャネル\_構成


KSPROPERTY\_オーディオ\_チャネル\_構成プロパティは、ノードを出力するオーディオ ストリームでチャネルの空間実際の配置を指定します。

## <span id="ddk_ksproperty_audio_channel_config_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHANNEL_CONFIG_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">取得</th>
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルターと Pin</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537083" data-raw-source="[&lt;strong&gt;KSAUDIO_CHANNEL_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537083)"><strong>KSAUDIO_CHANNEL_CONFIG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_チャネル\_構成します。 この構造体には、出力ストリームとスピーカーにこれらのチャネルの割り当てに含まれているチャネルを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_チャネル\_構成プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

DAC のノードのプロパティとして使用する場合 ([**KSNODETYPE\_DAC**](ksnodetype-dac.md)) または 3D のノード ([**KSNODETYPE\_3D\_効果** ](ksnodetype-3d-effects.md))、KSPROPERTY\_オーディオ\_チャネル\_構成プロパティが DirectSound スピーカーの構成を指定します。 組み合わせてこのプロパティを使用、ステレオのスピーカーの構成の場合、 [ **KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY** ](ksproperty-audio-stereo-speaker-geometry.md)プロパティで、ヘッドフォンとステレオのスピーカー構成がいくつかを区別します。 スピーカーの構成の詳細については、[DirectSound スピーカー構成設定](https://msdn.microsoft.com/library/windows/hardware/ff536332)を参照してください。

DirectSound は、では、KSPROPERTY\_オーディオ\_チャネル\_チャネル構成に対して「パン」ノードを照会するプロパティを構成します。 パン ノードはボリュームの 2 番目のノード ([**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)) を満たすミキサー ピン、 [DirectSound ノード順序要件](https://msdn.microsoft.com/library/windows/hardware/ff536331)します。 DirectSound 実装の**IDirectSoundBuffer::SetPan**メソッド (Microsoft Windows SDK のドキュメントで説明) はパン ノードの[ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](ksproperty-audio-volumelevel.md)パンを制御するプロパティ。

DirectSound 扱います KSPROPERTY\_オーディオ\_チャネル\_ボリュームと 3D のノードで pin のプロパティと、DAC のノード上のフィルター プロパティとして構成します。

クライアントは、ストリームの形式を選択するこのプロパティを使用する、 [ **KSNODETYPE\_PROLOGIC\_デコーダー** ](ksnodetype-prologic-decoder.md)ノードを出力します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSAUDIO\_チャネル\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff537083)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)

[**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)

[**KSPROPERTY\_AUDIO\_STEREO\_SPEAKER\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 






