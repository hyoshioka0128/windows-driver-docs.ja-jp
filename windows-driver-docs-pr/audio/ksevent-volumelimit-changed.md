---
title: KSEVENT\_VOLUMELIMIT\_変更されました
description: KSEVENT\_VOLUMELIMIT\_CHANGED イベントは、オーディオデバイスのオーディオボリュームレベルの制限が変更されたことをオーディオスタックに示します。
ms.assetid: CC6A6027-03CA-4D2C-8AA2-155E1617E19B
keywords:
- KSEVENT_VOLUMELIMIT_CHANGED オーディオデバイス
topic_type:
- apiref
api_name:
- KSEVENT_VOLUMELIMIT_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548f95309cfa8180983b36a137e6786f4a17db7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833103"
---
# <a name="ksevent_volumelimit_changed"></a>KSEVENT\_VOLUMELIMIT\_変更されました


KSEVENT\_VOLUMELIMIT\_CHANGED イベントは、オーディオデバイスのオーディオボリュームレベルの制限が変更されたことをオーディオスタックに示します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の種類 (操作データ) は、このイベントに使用する通知方法を指定する**KSEVENTDATA**構造体です。

<a name="remarks"></a>注釈
-------

KSEVENT\_PINCAPS\_VOLUMELIMITCHANGE イベントのサポートを実装する方法の詳細については、「 [**KSEVENT\_pincaps\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)」の「**解説**」を参照してください。

ただし、KSEVENT\_PINCAPS\_FORMATCHANGE が Wave フィルターに実装されていることに注意してください (Portcls にリンクされているミニポートドライバーの場合)、KSEVENT\_VOLUMELIMIT\_CHANGED イベントがトポロジフィルターに実装されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

 

 






