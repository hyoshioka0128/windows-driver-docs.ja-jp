---
title: KSPROPERTY\_オーディオ\_高音
description: KSPROPERTY\_オーディオ\_高音プロパティは、トーン ノードで、チャネルの音のレベルを指定します (KSNODETYPE\_トーン)。
ms.assetid: eee12fac-fbde-44d5-9172-538b9c486697
keywords:
- KSPROPERTY_AUDIO_TREBLE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_TREBLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac4cadba2ac75da490d44b63fd1811bb36c68e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578623"
---
# <a name="kspropertyaudiotreble"></a>KSPROPERTY\_オーディオ\_高音


KSPROPERTY\_オーディオ\_高音プロパティは、トーン ノードで、チャネルの音のレベルを指定します ([**KSNODETYPE\_トーン**](ksnodetype-tone.md))。

## <span id="ddk_ksproperty_audio_treble_ks"></span><span id="DDK_KSPROPERTY_AUDIO_TREBLE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型のチャネルの高音レベルの設定を指定します。 高音レベルの値は、次のスケールを使用します。

無限大デシベル (減衰) は-2147483648

-2147483647 は-32767.99998474 デシベル (減衰) と

+ 2147483647 までは、+32767.99998474 デシベル (向上です)。

整数値、比較的によって表されるデシベル範囲場所

このスケールでは、1/65536 デシベル精度があります。

フィルターには、フィルターの範囲を超えてはサポートされている範囲に値が固定される値を指定するプロパティの設定要求は成功します。 ただし、このプロパティを取得する後続の要求で、使用される実際の値を返すには。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_高音プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

トーン ノードでは、レベル、中間の頻度レベル、低音のレベルおよび音高音を制御するプロパティをサポートできます。 詳細については、次を参照してください。 [ **KSNODETYPE\_トーン**](ksnodetype-tone.md)します。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_トーン**](ksnodetype-tone.md)

 

 





