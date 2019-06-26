---
title: KSPROPERTY\_AC3\_代替\_オーディオ
description: KSPROPERTY\_AC3\_代替\_オーディオ プロパティは、ステレオのペアとして、または 2 つの独立したプログラム チャネルとして AC で 3 でエンコードされたストリームで 2 つの mono のチャネルを解釈するかどうかを指定します。
ms.assetid: fff2c52f-c996-4dfe-a46e-9f937cbd0d8c
keywords:
- KSPROPERTY_AC3_ALTERNATE_AUDIO オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ALTERNATE_AUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccefcc510bfaaaf3a172de410b52e6fd996ada4f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391527"
---
# <a name="kspropertyac3alternateaudio"></a>KSPROPERTY\_AC3\_代替\_オーディオ


KSPROPERTY\_AC3\_代替\_オーディオ プロパティは、ステレオのペアとして、または 2 つの独立したプログラム チャネルとして AC で 3 でエンコードされたストリームで 2 つの mono のチャネルを解釈するかどうかを指定します。

## <span id="ddk_ksproperty_ac3_alternate_audio_ks"></span><span id="DDK_KSPROPERTY_AC3_ALTERNATE_AUDIO_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_alternate_audio" data-raw-source="[&lt;strong&gt;KSAC3_ALTERNATE_AUDIO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_alternate_audio)"><strong>KSAC3_ALTERNATE_AUDIO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSAC3\_代替\_mono の 2 つのチャネルを解釈する方法を指定するオーディオ構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_代替\_オーディオ プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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

[**KSAC3\_ALTERNATE\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_alternate_audio)

 

 






