---
title: KSPROPERTY\_オーディオ\_動的\_範囲
description: KSPROPERTY\_オーディオ\_動的\_RANGE プロパティは、ラウドネスのノードから出力されるオーディオ ストリームの動的範囲を指定します (KSNODETYPE\_ラウドネス)。
ms.assetid: bab1cc2c-0751-4425-8546-9587baece585
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242b2ed692ea22360d724aa41b4b7eed04c2d1a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360625"
---
# <a name="kspropertyaudiodynamicrange"></a>KSPROPERTY\_オーディオ\_動的\_範囲


KSPROPERTY\_オーディオ\_動的\_RANGE プロパティは、ラウドネスのノードから出力されるオーディオ ストリームの動的範囲を指定します ([**KSNODETYPE\_ラウドネス**](ksnodetype-loudness.md)).

## <span id="ddk_ksproperty_audio_dynamic_range_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_RANGE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_dynamic_range" data-raw-source="[&lt;strong&gt;KSAUDIO_DYNAMIC_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_dynamic_range)"><strong>KSAUDIO_DYNAMIC_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_動的\_範囲のラウドネス ノードにストリームの出力の動的範囲を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_動的\_範囲プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

既定では、値によって、 **QuietCompression**と**LoudCompression** 、KSAUDIO のメンバー\_動的\_構造体の範囲は 0% に設定されます。 これには、オーディオ ストリームの完全なダイナミック レンジが生成されます。 ミニポート ドライバーは、データ パスを持つノードを含む暗証番号 (pin) をインスタンス化時に、既定値にプロパティを設定します。

一部のデバイスを変更できない場合があります**QuietCompression**と**LoudCompression**します。 クライアントが、デバイスがサポートされていない値を変更しようとすると、ミニポート ドライバーはエラーを返す必要があります。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ラウドネス**](ksnodetype-loudness.md)

[**KSAUDIO\_動的\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

 

 






