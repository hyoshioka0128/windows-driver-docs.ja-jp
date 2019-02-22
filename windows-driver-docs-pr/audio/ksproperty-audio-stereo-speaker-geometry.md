---
title: KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY
description: KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY プロパティは、KSPROPERTY と組み合わせて使用\_オーディオ\_チャネル\_CONFIG を実装する、ハードウェア アクセラレータを使用した 3D オーディオ DirectSound スピーカー構成プロパティ。
ms.assetid: 4a870368-6a9b-41bc-80c3-da6ad1f2454b
keywords:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 012135a9e435662b4a1de6b10abbf461f046942c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559078"
---
# <a name="kspropertyaudiostereospeakergeometry"></a>KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY


KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY プロパティと組み合わせて使用[ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](ksproperty-audio-channel-config.md)ハードウェア アクセラレータを使用した 3D オーディオ DirectSound スピーカー構成プロパティを実装します。 これは省略可能な DAC のノードのプロパティ ([**KSNODETYPE\_DAC**](ksnodetype-dac.md)) と 3D のノード ([**KSNODETYPE\_3D\_の効果**](ksnodetype-3d-effects.md)).

## <span id="ddk_ksproperty_audio_stereo_speaker_geometry_ks"></span><span id="DDK_KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY_KS"></span>


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
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin/フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型のスピーカーのジオメトリを指定します。 この値は、ヘッダー ファイル Ksmedia.h で定義されている次の定数のいずれかに設定できます。

-   KSAUDIO\_ステレオ\_スピーカー\_GEOMETRY\_ヘッドホン

-   KSAUDIO\_ステレオ\_スピーカー\_GEOMETRY\_MIN

-   KSAUDIO\_ステレオ\_スピーカー\_GEOMETRY\_ナロー

-   KSAUDIO\_ステレオ\_スピーカー\_GEOMETRY\_ワイド

-   KSAUDIO\_ステレオ\_スピーカー\_GEOMETRY\_MAX

これらのパラメーターは同じ意味であり (ただし、値に等しくない) を使用する、次の値を**IDirectSound::GetSpeakerConfig**メソッド (Microsoft Windows SDK のドキュメントを参照してください) に定義されていますヘッダー ファイル Dsound.h:

-   DSSPEAKER\_ヘッドホンによる立体音響

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_MIN

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_ナロー

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_ワイド

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_MAX

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound 扱います KSPROPERTY\_オーディオ\_ステレオ\_スピーカー\_GEOMETRY で DAC のノードでは、filter プロパティと 3D のノードに暗証番号 (pin) のプロパティとして。

詳細については、次を参照してください。 [DirectSound スピーカー構成設定](https://msdn.microsoft.com/library/windows/hardware/ff536332)します。

<a name="requirements"></a>要件
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


[**KSPROPERTY\_オーディオ\_チャネル\_構成**](ksproperty-audio-channel-config.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






