---
title: KSEVENT\_PINCAPS\_JACKINFOCHANGE
description: KSEVENT\_PINCAPS\_JACKINFOCHANGE イベント オーディオ デバイスのジャック情報が変更されたことをオーディオ スタックを示します。
ms.assetid: 46514043-5044-4373-94ca-b00898aeefba
keywords:
- KSEVENT_PINCAPS_JACKINFOCHANGE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSEVENT_PINCAPS_JACKINFOCHANGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7289f5dcebb1d4b1fa0db26bbe8470f4bd9aa35f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333369"
---
# <a name="kseventpincapsjackinfochange"></a>KSEVENT\_PINCAPS\_JACKINFOCHANGE


`KSEVENT_PINCAPS_JACKINFOCHANGE`イベント オーディオ デバイスのジャック情報が変更されたことをオーディオ スタックを示します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の型 (データの操作) は、 **KSEVENTDATA**をこのイベントに使用する通知方法を指定します。

<a name="remarks"></a>注釈
-------

サポートを実装する方法については、`KSEVENT_PINCAPS_JACKINFOCHANGE`イベントの「解説」を参照してください、 [ **KSEVENT\_PINCAPS\_段落**](ksevent-pincaps-formatchange.md)トピック。

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
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**KSEVENT\_PINCAPS\_段落**](ksevent-pincaps-formatchange.md)

 

 






