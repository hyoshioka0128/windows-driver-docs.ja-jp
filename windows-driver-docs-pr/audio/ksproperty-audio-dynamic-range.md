---
title: KSK プロパティ\_AUDIO\_動的\_範囲
description: KSK プロパティ\_AUDIO\_DYNAMIC\_RANGE プロパティは、ラウドネスノード (KSNODETYPE\_ラウドネス) から出力されるオーディオストリームの動的な範囲を指定します。
ms.assetid: bab1cc2c-0751-4425-8546-9587baece585
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE オーディオデバイス
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
ms.openlocfilehash: c2a26ac744347cf45965702bcf00509c97752e56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831042"
---
# <a name="ksproperty_audio_dynamic_range"></a>KSK プロパティ\_AUDIO\_動的\_範囲


KSK プロパティ\_AUDIO\_DYNAMIC\_RANGE プロパティは、ラウドネスノード ([**KSNODETYPE\_ラウドネス**](ksnodetype-loudness.md)) から出力されるオーディオストリームの動的な範囲を指定します。

## <span id="ddk_ksproperty_audio_dynamic_range_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_RANGE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range" data-raw-source="[&lt;strong&gt;KSAUDIO_DYNAMIC_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)"><strong>KSAUDIO_DYNAMIC_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、"KSAUDIO\_動的\_範囲の構造であり、ラウドネスノードの出力ストリームの動的範囲を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_動的\_範囲のプロパティ要求\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

既定では、KSK オーディオ\_動的\_範囲構造の**値はゼロ**% に設定されます。 これにより、オーディオストリームの完全な動的範囲が生成されます。 ミニポートドライバーは、データパスにノードが含まれている pin をインスタンス化するときに、プロパティを既定値に設定します。

一部のデバイスでは、 **QuietCompression**および**LoudCompression**への変更がサポートされていない場合があります。 デバイスでサポートされていない値をクライアントが変更しようとすると、ミニポートドライバーからエラーが返されます。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ラウドネス**](ksnodetype-loudness.md)

[**KSAUDIO\_動的\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

 

 






