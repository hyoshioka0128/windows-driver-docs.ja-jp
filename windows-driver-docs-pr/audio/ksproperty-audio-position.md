---
title: KSK プロパティ\_オーディオ\_位置
description: KSK プロパティ\_AUDIO\_POSITION プロパティは、ピンのオーディオストリームのサウンドバッファー内の再生カーソルと書き込みカーソルの現在の位置を指定します。
ms.assetid: 859990bc-18c0-429a-afb6-07b5adc98630
keywords:
- KSPROPERTY_AUDIO_POSITION オーディオデバイス
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
ms.openlocfilehash: 6fda4fdde2bf7bb6d2863a054011c71a1a892309
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830947"
---
# <a name="ksproperty_audio_position"></a>KSK プロパティ\_オーディオ\_位置


KSK プロパティ\_AUDIO\_POSITION プロパティは、ピンのオーディオストリームのサウンドバッファー内の再生カーソルと書き込みカーソルの現在の位置を指定します。

## <span id="ddk_ksproperty_audio_position_ks"></span><span id="DDK_KSPROPERTY_AUDIO_POSITION_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)"><strong>KSAUDIO_POSITION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、型 KSAUDIO\_POSITION の構造体であり、レンダリングストリームの再生位置と書き込み位置、またはキャプチャストリームのレコードと読み取り位置を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_POSITION プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound では、KSK プロパティ\_AUDIO\_POSITION プロパティを使用して、 **Idirectsoundbuffer:: GetCurrentPosition**メソッドと**Idirectsoundbuffer:: SetCurrentPosition**メソッドを実装します。 Windows マルチメディア関数**waveInGetPosition**と**waveOutGetPosition**は、このプロパティも使用します。 DirectSound と Windows マルチメディア機能の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

WaveCyclic および WavePci ミニポートドライバーは、KSK プロパティ\_オーディオ\_位置のプロパティハンドラーを実装する必要はありません。これは、WaveCyclic および WavePci ポートドライバーがミニポートドライバーに代わってこのプロパティを処理するためです。 キャプチャストリーム内のレンダーストリームまたはレコード位置で再生位置を取得するには、ポートドライバーのプロパティハンドラーが、ミニポートドライバーの[**IMiniportWaveCyclicStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)または[**IMiniportWavePciStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)を呼び出します。b.

詳細については、「 [Audio Position プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-position-property)」を参照してください。

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
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)

[**IMiniportWaveCyclicStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)

 

 






