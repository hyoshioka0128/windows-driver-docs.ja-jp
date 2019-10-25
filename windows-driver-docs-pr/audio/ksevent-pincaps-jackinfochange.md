---
title: KSEVENT\_PINCAPS\_JACKINFOCHANGE
description: KSEVENT\_PINCAPS\_JACKINFOCHANGE イベントは、オーディオデバイスのジャック情報が変更されたことをオーディオスタックに示します。
ms.assetid: 46514043-5044-4373-94ca-b00898aeefba
keywords:
- KSEVENT_PINCAPS_JACKINFOCHANGE オーディオデバイス
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
ms.openlocfilehash: 995ad652db0d56fb71c1fb514b5e9ecfe868b12d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833119"
---
# <a name="ksevent_pincaps_jackinfochange"></a>KSEVENT\_PINCAPS\_JACKINFOCHANGE


`KSEVENT_PINCAPS_JACKINFOCHANGE` イベントは、オーディオデバイスのジャック情報が変更されたことをオーディオスタックに示します。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の種類 (操作データ) は、このイベントに使用する通知方法を指定する**KSEVENTDATA**構造体です。

<a name="remarks"></a>注釈
-------

`KSEVENT_PINCAPS_JACKINFOCHANGE` イベントのサポートを実装する方法の詳細については、「 [**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md) 」トピックの「解説」セクションを参照してください。

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
<td align="left"><p>Windows 7 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)

 

 






