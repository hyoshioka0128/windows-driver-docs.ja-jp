---
title: KSK プロパティ\_テレフォニー\_CALLINFO
description: 呼び出しの状態や呼び出しの種類など、現在の呼び出し情報を取得するには、KSK プロパティ\_TELEPHONY\_CALLINFO プロパティを使用します。
ms.assetid: EEBA38F6-86EC-4C2C-930C-A848153AD918
keywords:
- KSPROPERTY_TELEPHONY_CALLINFO オーディオデバイス
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
ms.openlocfilehash: 27c61e416bd30d242155a441375355d997b7c74e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830480"
---
# <a name="ksproperty_telephony_callinfo"></a>KSK プロパティ\_テレフォニー\_CALLINFO


呼び出しの状態や呼び出しの種類など、現在の呼び出し情報を取得するには、 **Ksk プロパティ\_TELEPHONY\_CALLINFO**プロパティを使用します。

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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)"><strong>KSTELEPHONY_CALLINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は[**KSTELEPHONY\_CALLINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)で、電話の状態と種類を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**\_テレフォニー\_CALLINFO** property 要求では、呼び出しの種類 (LTE パケットスイッチ、WLAN パケットスイッチ、またはサーキットスイッチ) と呼び出しの状態 () を含む[**KSTELEPHONY\_callinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callinfo)構造体が返されます。有効、無効、保持、またはプロバイダの移行中)。

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

 

 





