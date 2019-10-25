---
title: KSK プロパティ\_テレフォニー\_CALLHOLD
description: "\"KSK プロパティ\\_テレフォニー\\_CALLHOLD\" プロパティは、通話の保留状態を制御するために使用されます。"
ms.assetid: C683A6AA-35E5-43D3-B882-B13B8A0A4043
keywords:
- KSPROPERTY_TELEPHONY_CALLHOLD オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLHOLD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3274d81de9894e166b574581f3357d4ddc9f5b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832711"
---
# <a name="ksproperty_telephony_callhold"></a>KSK プロパティ\_テレフォニー\_CALLHOLD


" **Ksk プロパティ\_テレフォニー\_CALLHOLD** " プロパティは、通話の保留状態を制御するために使用されます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は BOOL で、通話が保留中かどうかを指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**TELEPHONY プロパティ\_TELEPHONY\_CALLHOLD**プロパティ要求は、での呼び出しが保留になっている場合に**TRUE**を返します。それ以外の場合は**FALSE**を返します。

<a name="remarks"></a>注釈
-------

値が**TRUE**の場合は、 **KSK プロパティ\_TELEPHONY\_callhold**プロパティに設定した場合、電話は保留の状態になります。 予想される動作は、送信と受信の両方がミュートになることです。 この場合、データは送信または受信されません。 オーディオドライバーは、通話状態 ([**テレフォニー\_callstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callstate)) を**テレフォニー\_CALLSTATE\_保持**するように更新します。 値を**FALSE**に設定した場合、 **KSK プロパティ\_テレフォニー\_callhold**プロパティに設定すると、電話は保留状態のままになり、通話状態が**テレフォニー\_callhold\_有効**に更新されます。

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

 

 





