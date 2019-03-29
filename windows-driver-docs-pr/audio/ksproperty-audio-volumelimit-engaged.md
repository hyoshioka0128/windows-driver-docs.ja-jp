---
title: KSPROPERTY\_オーディオ\_VOLUMELIMIT\_関心度の高い
description: KSPROPERTY\_オーディオ\_VOLUMELIMIT\_、KSPROPSETID に追加されている新しい KS プロパティには、\_オーディオ プロパティが Windows 8.1 に設定します。
ms.assetid: 0DAC584A-EC17-4280-B90D-2D9DDB620479
keywords:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4c5432521ee9343723805b5ab5ced22ed5c518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582675"
---
# <a name="kspropertyaudiovolumelimitengaged"></a>KSPROPERTY\_オーディオ\_VOLUMELIMIT\_関心度の高い


KSPROPERTY\_オーディオ\_VOLUMELIMIT\_、KSPROPSETID に追加されている新しい KS プロパティには、\_オーディオ プロパティが Windows 8.1 に設定します。

KSPROPERTY\_オーディオ\_VOLUMELIMIT\_関心度の高いプロパティ要求は、基になるドライバーをエンドユーザーのボリューム レベルの制限の設定を渡します。 このプロパティのスコープは、pin ごと (またはエンドユーザーの観点から、オーディオのエンドポイントごと)。

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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>暗証番号 (pin) のインスタンス</p></td>
<td align="left"><p>KSP_PIN</p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値型、BOOL、エンドユーザーが特定の制限を超える最大ボリュームをできるかどうかを示します。 TRUE の値は、ことをエンドユーザーは許可されているボリューム レベルに、ポストされた制限するのには逆の場合は false を示します。 お子様のアカウントの場合、値は FALSE を常になります。

ドライバーは、内部変数にこのプロパティの値を格納し、起動中を TRUE に値を初期化します。 このプロパティが TRUE の場合、ドライバーは、ボリュームの最大レベルを制限します。 プロパティが FALSE に設定されている場合、ドライバーは、これらの制限を削除できます。

ドライバーはこのプロパティの値を自動的に変更もできます。 たとえば、ドライバーからプロパティの値を FALSE、true を自動的に切り替えるし、ある程度の特定のサウンドのレベルを超過時間が経過した後、ボリューム レベルを制限することを開始します。

プロパティの値が変更されるたびに関係なく自動かどうか、または呼び出し元が、プロパティ値の設定により、ドライバー生成する、KSEVENT\_PINCAPS\_VOLUMELIMITCHANGE イベント。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_VOLUMELIMIT\_関心度の高いプロパティ要求がステータスを返します\_成功要求が正常に完了します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





