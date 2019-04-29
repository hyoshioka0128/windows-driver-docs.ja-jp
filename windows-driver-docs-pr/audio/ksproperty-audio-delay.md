---
title: KSPROPERTY\_オーディオ\_遅延
description: KSPROPERTY\_オーディオ\_遅延プロパティは、タイム ラグを示します。 その遅延ノード (KSNODETYPE\_遅延) に指定したチャネルが導入されています。
ms.assetid: ac260b83-1d7c-49d7-b325-ea0f21646d39
keywords:
- KSPROPERTY_AUDIO_DELAY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DELAY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7122df9cac0bc88c34729fb446c126c709891c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333075"
---
# <a name="kspropertyaudiodelay"></a>KSPROPERTY\_オーディオ\_遅延


KSPROPERTY\_オーディオ\_遅延プロパティは、タイム ラグを示します。 その遅延ノード ([**KSNODETYPE\_遅延**](ksnodetype-delay.md)) は、指定したチャネルに導入します。

## <span id="ddk_ksproperty_audio_delay_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DELAY_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567145" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567145)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、タイム ラグのサイズを指定します、KSTIME 型の構造です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_遅延プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSTIME**](https://msdn.microsoft.com/library/windows/hardware/ff567145)

[**KSNODETYPE\_遅延**](ksnodetype-delay.md)

 

 






