---
title: KSPROPERTY\_オーディオ\_位置
description: KSPROPERTY\_オーディオ\_位置プロパティは、pin のオーディオ ストリームのサウンド バッファーで再生および書き込みカーソルの現在の位置を指定します。
ms.assetid: 859990bc-18c0-429a-afb6-07b5adc98630
keywords:
- KSPROPERTY_AUDIO_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b955c6fa76a549a95e6f935ff04f3646ac229e91
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391464"
---
# <a name="kspropertyaudioposition"></a>KSPROPERTY\_オーディオ\_位置


KSPROPERTY\_オーディオ\_位置プロパティは、pin のオーディオ ストリームのサウンド バッファーで再生および書き込みカーソルの現在の位置を指定します。

## <span id="ddk_ksproperty_audio_position_ks"></span><span id="DDK_KSPROPERTY_AUDIO_POSITION_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position)"><strong>KSAUDIO_POSITION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_レンダリング ストリームの再生位置またはキャプチャ ストリームのレコードの書き込みし、読み取り位置を指定する位置。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_位置プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

DirectSound は、KSPROPERTY\_オーディオ\_POSITION プロパティを実装する、 **IDirectSoundBuffer::GetCurrentPosition**と**IDirectSoundBuffer::SetCurrentPosition**メソッド。 Windows のマルチ メディア機能**waveInGetPosition**と**waveOutGetPosition**もこのプロパティを使用します。 DirectSound と Windows のマルチ メディア機能の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

WaveCyclic と WavePci のミニポート ドライバーは KSPROPERTY のプロパティのハンドラーを実装する必要はありません\_オーディオ\_WaveCyclic と WavePci ポート ドライバー ミニポート ドライバーの代わりにこのプロパティを処理するために配置します。 ポート ドライバー プロパティ ハンドラーが、ミニポート ドライバーを呼び出すレンダリング ストリームの再生位置またはキャプチャ ストリーム内のレコードの位置を取得する[ **IMiniportWaveCyclicStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)または[ **IMiniportWavePciStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)メソッド。

詳細については、次を参照してください。[オーディオ位置プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-position-property)します。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position)

[**IMiniportWaveCyclicStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)

 

 






