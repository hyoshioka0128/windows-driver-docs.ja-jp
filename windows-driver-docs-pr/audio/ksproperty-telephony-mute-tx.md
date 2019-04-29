---
title: KSPROPERTY\_テレフォニー\_ミュート\_TX
description: KSPROPERTY\_テレフォニー\_ミュート\_TX プロパティを使用して、リモートの末尾にローカルのマイクから送信されるデータをミュートするかどうかを制御します。
ms.assetid: FB59AFB8-A11D-4E8D-9C39-131F1D807D4A
keywords:
- KSPROPERTY_TELEPHONY_MUTE_TX オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_MUTE_TX
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4965eddcb5ee9039896ef2861bd8a1809f69ccb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332572"
---
# <a name="kspropertytelephonymutetx"></a>KSPROPERTY\_テレフォニー\_ミュート\_TX


**KSPROPERTY\_テレフォニー\_ミュート\_TX**リモートの末尾にローカルのマイクから送信されるデータをミュートするかどうかを制御するプロパティを使用します。

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
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は BOOL 型で、ローカルのマイクとリモート エンドで表示されるデータから送信されるデータがミュートされているかどうかを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_ミュート\_TX**プロパティ要求を返します**TRUE**場合は、電話をかけるをミュート返します**FALSE**、電話をかけるがミュートされてない場合。

<a name="requirements"></a>必要条件
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

 

 





