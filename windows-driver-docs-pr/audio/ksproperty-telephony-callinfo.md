---
title: KSPROPERTY\_テレフォニー\_CALLINFO
description: KSPROPERTY\_テレフォニー\_CALLINFO プロパティを使用して、呼び出しの状態と呼び出しの種類など、現在の呼び出し情報を取得します。
ms.assetid: EEBA38F6-86EC-4C2C-930C-A848153AD918
keywords:
- KSPROPERTY_TELEPHONY_CALLINFO オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 357bd54dc2f59762fdbc53e6f594c2a2213e38d3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391576"
---
# <a name="kspropertytelephonycallinfo"></a>KSPROPERTY\_テレフォニー\_CALLINFO


**KSPROPERTY\_テレフォニー\_CALLINFO**呼び出しの状態と呼び出しの種類など、現在の呼び出し情報を取得するプロパティを使用します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callinfo" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)"><strong>KSTELEPHONY_CALLINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型[ **KSTELEPHONY\_CALLINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)状態と、電話の種類を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_CALLINFO**プロパティ要求を返します、 [ **KSTELEPHONY\_CALLINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)される構造呼び出しの種類 (LTE パケット交換 WLAN パケット交換または回線交換) が含まれていて、呼び出しの状態 (有効、無効になっている、保持されている、またはプロバイダーの移行中)。

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

 

 





