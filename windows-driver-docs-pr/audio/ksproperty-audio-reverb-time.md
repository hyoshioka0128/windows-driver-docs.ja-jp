---
title: KSPROPERTY\_オーディオ\_リバーブ\_時間
description: KSPROPERTY\_オーディオ\_リバーブ\_時のプロパティがリバーブ時間を指定します。 これはリバーブ ノードのプロパティ (KSNODETYPE\_リバーブ)。
ms.assetid: ADB53E00-4E0F-4E13-92C7-5ACB1A0B546E
keywords:
- KSPROPERTY_AUDIO_REVERB_TIME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_REVERB_TIME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 617fbed6b1e061f02a806d9ce96185306030c423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332950"
---
# <a name="kspropertyaudioreverbtime"></a>KSPROPERTY\_オーディオ\_リバーブ\_時間


KSPROPERTY\_オーディオ\_リバーブ\_時のプロパティがリバーブ時間を指定します。 これはリバーブ ノードのプロパティ ([**KSNODETYPE\_リバーブ**](ksnodetype-reverb.md))。

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
<td align="left"><p>KSNODEPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値、ULONG 型、反響を続行する秒数を指定します。 秒単位で表現され、1/256 単位 255.9961 を通じて、値の範囲は 0。 これに合わせて、プロパティの値を次が true、固定小数点 16.16 値として表現されなければなりません。

-   0x00010000 値は、1 秒を表します。
-   値が 0 xffffffff (65536-1/65536) を表します (秒)

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_リバーブ\_時間プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_リバーブ**](ksnodetype-reverb.md)

 

 






