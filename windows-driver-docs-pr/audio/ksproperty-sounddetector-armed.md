---
title: KSPROPERTY\_SOUNDDETECTOR\_故障
description: KSPROPERTY\_SOUNDDETECTOR\_腕プロパティは、検出機能の現在の arming 状態。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664F
keywords:
- KSPROPERTY_SOUNDDETECTOR_ARMED オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_ARMED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce1c9e03026548fcfec933dc0bfd6a7c940a0d1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539329"
---
# <a name="kspropertysounddetectorarmed"></a>KSPROPERTY\_SOUNDDETECTOR\_故障


**KSPROPERTY\_SOUNDDETECTOR\_故障**プロパティは、検出機能の現在の arming 状態。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティの値は、arming、検出機能の状態を示すブール値です。

<a name="remarks"></a>注釈
-------

OS 設定との連携する場合は true、検出機能。

ドライバーはこの場合に false にリセットします。

-   フィルター インターフェイスは無効です。
-   [ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)プロパティを設定します。
-   キーワードが検出されました。

キーワードのパターンが設定されていないときに、この true を設定 ([**KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)が空) 影響を与えません。
&gt; \[!注\]&gt;このプロパティが true の場合、その後設定[ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)にこれが自動的にリセットfalse、上記のとおりです。

 

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


[**KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






