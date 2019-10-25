---
title: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED
description: 一致が検出されるたびに OS に通知するために、オーディオドライバーによって生成される KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED イベントが生成されます。
ms.assetid: 595EBC90-3903-495C-9811-A47B7BC4D98D
keywords:
- KSEVENT_SOUNDDETECTOR_MATCHDETECTED オーディオデバイス
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
ms.openlocfilehash: 9952f5a13e55eb9049c8e1254ad389b46446bf0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833106"
---
# <a name="ksevent_sounddetector_matchdetected"></a>KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED


一致が検出されるたびに OS に通知するために、オーディオドライバーによって生成される**KSEVENT\_SOUNDDETECTOR\_matchdetected**イベントが生成されます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このイベントがトリガーされると、OS は、 [ **\_MATCHRESULT プロパティの Ksk プロパティ\_SOUNDDETECTOR**](ksproperty-sounddetector-matchresult.md)を読み取ります。 オーディオドライバーは、一致が検出された後、サウンド検出機能を無効にする必要があります。 もう一度待機する準備ができたら、OS はデバイスを再アームします。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[ **\_MATCHRESULT の KSK プロパティ\_SOUNDDETECTOR**](ksproperty-sounddetector-matchresult.md)

 

 






