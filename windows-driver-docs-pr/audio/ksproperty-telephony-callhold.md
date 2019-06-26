---
title: KSPROPERTY\_テレフォニー\_CALLHOLD
description: KSPROPERTY\_テレフォニー\_CALLHOLD プロパティは、通話の保留状態の制御に使用されます。
ms.assetid: C683A6AA-35E5-43D3-B882-B13B8A0A4043
keywords:
- KSPROPERTY_TELEPHONY_CALLHOLD オーディオ デバイス
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
ms.openlocfilehash: f65512e3100ffcfc2410379639d8a77a07d87ca4
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391592"
---
# <a name="kspropertytelephonycallhold"></a>KSPROPERTY\_テレフォニー\_CALLHOLD


**KSPROPERTY\_テレフォニー\_CALLHOLD**通話の保留中の状態を制御するプロパティを使用します。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は BOOL 型の電話呼び出しが保留中かどうかを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_CALLHOLD**プロパティ要求を返します**TRUE**場合上での通話の保留以外を返しますそれ以外の場合、 **FALSE**します。

<a name="remarks"></a>注釈
-------

設定した場合、 **KSPROPERTY\_テレフォニー\_CALLHOLD**プロパティの値を持つ**TRUE**、電話呼び出しは保留中に配置されます。 想定される動作は、送信と受信の両方をミュートすることです。 データはありませんは、送信または受信をここでは。 オーディオ ドライバーは、呼び出しの状態を更新 ([**テレフォニー\_CALLSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-telephony_callstate)) に**テレフォニー\_CALLSTATE\_保持**します。 設定した場合、 **KSPROPERTY\_テレフォニー\_CALLHOLD**プロパティの値を持つ**FALSE**、電話呼び出しが保留中の状態から取得され、呼び出しの状態が更新され**テレフォニー\_CALLSTATE\_有効**します。

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

 

 





