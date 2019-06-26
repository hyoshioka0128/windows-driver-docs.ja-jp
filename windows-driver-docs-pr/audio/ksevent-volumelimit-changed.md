---
title: KSEVENT\_VOLUMELIMIT\_CHANGED
description: KSEVENT\_VOLUMELIMIT\_オーディオ デバイスのオーディオ ボリューム レベルの制限が変更されたこと、オーディオ スタックに CHANGED イベントを示します。
ms.assetid: CC6A6027-03CA-4D2C-8AA2-155E1617E19B
keywords:
- KSEVENT_VOLUMELIMIT_CHANGED オーディオ デバイス
topic_type:
- apiref
api_name:
- KSEVENT_VOLUMELIMIT_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96ac4f7cf4078420efd7464a519699ad0be3d000
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391518"
---
# <a name="kseventvolumelimitchanged"></a>KSEVENT\_VOLUMELIMIT\_CHANGED


KSEVENT\_VOLUMELIMIT\_オーディオ デバイスのオーディオ ボリューム レベルの制限が変更されたこと、オーディオ スタックに CHANGED イベントを示します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span> 使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">対象</th>
<th align="left">イベント記述子の種類</th>
<th align="left">イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の型 (データの操作) は、 **KSEVENTDATA**をこのイベントに使用する通知方法を指定します。

<a name="remarks"></a>注釈
-------

KSEVENT のサポートを実装する方法については\_PINCAPS\_VOLUMELIMITCHANGE イベントを参照してください、**解説**の[ **KSEVENT\_PINCAPS\_段落**](ksevent-pincaps-formatchange.md)します。

KSEVENT 中に注意して\_PINCAPS\_(ミニポート ドライバーに Portcls にリンクされている)、Wave フィルターが実装されている段落、KSEVENT\_VOLUMELIMIT\_CHANGED イベントは、トポロジの実装フィルターです。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENT\_PINCAPS\_段落**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)

 

 






