---
title: KSPROPERTY\_AC3\_ビット\_ストリーム\_モード
description: KSPROPERTY\_AC3\_ビット\_ストリーム\_モード プロパティをビット ストリーム モードで、ac-3 ストリームにエンコードされたオーディオのサービスの種類を指定します。
ms.assetid: ee3705f5-f16d-4f5e-a551-bea8986d88b6
keywords:
- KSPROPERTY_AC3_BIT_STREAM_MODE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_BIT_STREAM_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b08f9752eb65493157589ff50c2e58f5d219b40f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391524"
---
# <a name="kspropertyac3bitstreammode"></a>KSPROPERTY\_AC3\_ビット\_ストリーム\_モード


KSPROPERTY\_AC3\_ビット\_ストリーム\_モード プロパティをビット ストリーム モードで、ac-3 ストリームにエンコードされたオーディオのサービスの種類を指定します。

## <span id="ddk_ksproperty_ac3_bit_stream_mode_ks"></span><span id="DDK_KSPROPERTY_AC3_BIT_STREAM_MODE_KS"></span>


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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_bit_stream_mode" data-raw-source="[&lt;strong&gt;KSAC3_BIT_STREAM_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)"><strong>KSAC3_BIT_STREAM_MODE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSAC3\_ビット\_ストリーム\_モード構造体のビット ストリーム モードを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_ビット\_ストリーム\_モード プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAC3\_ビット\_ストリーム\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)

 

 






