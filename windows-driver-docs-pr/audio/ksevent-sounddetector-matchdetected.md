---
title: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED
description: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED イベントは一致が検出されたときに、OS に通知するオーディオ ドライバーによって生成されます。
ms.assetid: 595EBC90-3903-495C-9811-A47B7BC4D98D
keywords:
- KSEVENT_SOUNDDETECTOR_MATCHDETECTED オーディオ デバイス
topic_type:
- apiref
api_name:
- KSEVENT_SOUNDDETECTOR_MATCHDETECTED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd0672523ef095af5541dbe38923df887846f8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549811"
---
# <a name="kseventsounddetectormatchdetected"></a>KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED


**KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED**一致が検出されたときに、OS に通知するオーディオ ドライバーによってイベントが生成されました。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このイベントがトリガーされたときに、OS を読み取り、 [ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)プロパティ。 一致が検出された後、オーディオ ドライバーは、サウンドの検出機能を解除する必要があります。 OS はデバイスを rearms 準備が整ったら再度待つ。

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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






