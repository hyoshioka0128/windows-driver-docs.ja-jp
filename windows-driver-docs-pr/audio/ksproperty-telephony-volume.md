---
title: KSPROPERTY\_テレフォニー\_ボリューム
description: KSPROPERTY\_テレフォニー\_ボリュームのプロパティを使用して、携帯電話のすべての呼び出しの量を制御します。
ms.assetid: 3754A7A0-FA50-4831-B449-DED0D3D69418
keywords:
- KSPROPERTY_TELEPHONY_VOLUME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8911068ddd02bbf30434394ce495d554b8501d08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528432"
---
# <a name="kspropertytelephonyvolume"></a>KSPROPERTY\_テレフォニー\_ボリューム


**KSPROPERTY\_テレフォニー\_ボリューム**プロパティを使用して、携帯電話のすべての呼び出しの量を制御します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は LONG 型の携帯電話の呼び出しのボリュームを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_ボリューム**プロパティ要求が携帯電話の数を返します。

<a name="remarks"></a>注釈
-------

携帯電話の呼び出しに対してのみ、このボリュームは、携帯電話のデータに適用され、エンドポイントのボリュームが影響を与えません。 このプロパティは、システムでアクティブな電話呼び出しがない場合でも、設定可能にする必要があります。 このプロパティの基本的なサポートは、最小のボリューム、最大のボリュームとボリュームの範囲を返す必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





