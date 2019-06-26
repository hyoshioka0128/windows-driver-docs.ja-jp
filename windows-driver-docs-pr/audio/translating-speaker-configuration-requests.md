---
title: スピーカー構成の要求を変換
description: スピーカー構成の要求を変換
ms.assetid: be3dce30-7395-4332-ba62-de9a718b62f5
keywords:
- スピーカー構成要求の WDK オーディオを翻訳します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42f30166f6e88a552b113b532ae77272cfcfab07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354167"
---
# <a name="translating-speaker-configuration-requests"></a>スピーカー構成の要求を変換


## <span id="translating_speaker_configuration_requests"></span><span id="TRANSLATING_SPEAKER_CONFIGURATION_REQUESTS"></span>


**注**  この情報は、Windows XP およびそれ以前のオペレーティング システムに適用されます。 以降、Windows Vista で**IDirectSound::GetSpeakerConfig**と**IDirectSound::SetSpeakerConfig**非推奨とされました。

 

アプリケーションを呼び出すと**IDirectSound::SetSpeakerConfig** (参照 Microsoft Windows SDK のドキュメント)、DirectSound のスピーカー構成を変更する変換指定 DSSPEAKER\_*Xxx*スピーカー構成パラメーターと同じ KSAUDIO に\_*Xxx*チャネル構成マスク。 送信、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config) DirectSound デバイスを表すフィルターには、このマスクを含むプロパティの設定要求。

次の表では、各 DSSPEAKER\_*Xxx*左側のパラメーターは同等の KSAUDIO と組み合わせて使用\_*Xxx*右側のチャネル構成マスク。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER パラメーター</th>
<th align="left">KSAUDIO チャネル構成マスク</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DSSPEAKER_DIRECTOUT</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_DIRECTOUT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_HEADPHONE</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_STEREO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_MONO</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_MONO</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_STEREO</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_STEREO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_QUAD</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_QUAD</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_SURROUND</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_SURROUND</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_5POINT1</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_7POINT1</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1</p></td>
</tr>
</tbody>
</table>

 

上記の表に、DirectSound は KSAUDIO などについては、同じチャネル マスクを持つそのヘッドホンによる立体音響とステレオのスピーカーの構成を指定します\_スピーカー\_ステレオします。 これら 2 つの構成を区別するために DirectSound 送信フィルター スピーカー ジオメトリを指定します 2 番目のプロパティの設定要求 (を参照してください[ **KSPROPERTY\_オーディオ\_ステレオ\_。スピーカー\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-stereo-speaker-geometry))。 ヘッドホンを示すためには、DirectSound は KSAUDIO の値を渡します。\_ステレオ\_スピーカー\_GEOMETRY\_ヘッドホンによる立体音響スピーカー geometry 要求。

ステレオ スピーカー、ただし、呼び出し元が場合**SetSpeakerConfig**可能 DSSPEAKER をいくつかのいずれかを指定できます\_*Xxx*ステレオのスピーカーのジオメトリ。 これらの次の表と同等の KSAUDIO 左の列には表示\_*Xxx*パラメーターは、右側に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER ステレオのスピーカー Geometry</th>
<th align="left">KSAUDIO ステレオのスピーカー Geometry</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DSSPEAKER_GEOMETRY_WIDE</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_WIDE</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_GEOMETRY_NARROW</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_NARROW</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_GEOMETRY_MIN</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_MIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_GEOMETRY_MAX</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_MAX</p></td>
</tr>
</tbody>
</table>

 

DirectSound DSSPEAKER 前提としています、呼び出し元が指定しない場合に明示的にジオメトリのいずれかの上、左の列で、\_GEOMETRY\_既定ではさまざまです。

 

 




