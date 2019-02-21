---
title: KSPROPERTY\_オーディオ\_コーラス\_変調\_深さ
description: KSPROPERTY\_オーディオ\_コーラス\_変調\_DEPTH プロパティをコーラス変調深さを指定します。 これはコーラス ノードのプロパティ (KSNODETYPE\_コーラス)。
ms.assetid: A14DA707-7ED6-4E86-87C7-9A4E40062FE8
keywords:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59517963e67bb31a94db8267cf1c7578826f2bb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528557"
---
# <a name="kspropertyaudiochorusmodulationdepth"></a>KSPROPERTY\_オーディオ\_コーラス\_変調\_深さ


KSPROPERTY\_オーディオ\_コーラス\_変調\_DEPTH プロパティをコーラス変調深さを指定します。 これはコーラス ノードのプロパティ ([**KSNODETYPE\_コーラス**](ksnodetype-chorus.md))。

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

 

ULONG 型のプロパティの値は、コーラス変調深さを指定します。 ミリ秒単位でし、モジュレーターの速度 (頻度) を設定します。 値の範囲は 0 から 1/256 単位 255.9961 です。 これに合わせて、プロパティの値を次が true、固定小数点 16.16 値として表現されなければなりません。

-   0x00010000 値 1 を表す ms
-   値が 0 xffffffff (65536-1/65536) を表す ms

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_コーラス\_変調\_深さプロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODETYPE\_コーラス**](ksnodetype-chorus.md)

 

 






