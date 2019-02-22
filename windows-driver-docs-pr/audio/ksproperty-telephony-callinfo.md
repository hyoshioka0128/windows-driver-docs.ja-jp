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
ms.openlocfilehash: c35079702e61b65a659d1c83839e8971e1d65226
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551688"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169884" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169884)"><strong>KSTELEPHONY_CALLINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型[ **KSTELEPHONY\_CALLINFO**](https://msdn.microsoft.com/library/windows/hardware/mt169884)状態と、電話の種類を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_CALLINFO**プロパティ要求を返します、 [ **KSTELEPHONY\_CALLINFO** ](https://msdn.microsoft.com/library/windows/hardware/mt169884)される構造呼び出しの種類 (LTE パケット交換 WLAN パケット交換または回線交換) が含まれていて、呼び出しの状態 (有効、無効になっている、保持されている、またはプロバイダーの移行中)。

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

 

 





