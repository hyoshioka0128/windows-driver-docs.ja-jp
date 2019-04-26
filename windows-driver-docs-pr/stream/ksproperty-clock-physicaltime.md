---
title: KSPROPERTY\_クロック\_PHYSICALTIME
description: クライアントの使用、KSPROPERTY\_クロック\_物理\_クロックの現在の物理的な時間を決定時のプロパティ。
ms.assetid: cc747fd4-1df0-4d44-b43e-b43532c1228b
keywords:
- KSPROPERTY_CLOCK_PHYSICALTIME ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_PHYSICALTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6acdc9700f040d9cd2ee4e9f901fff31b81e0ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357056"
---
# <a name="kspropertyclockphysicaltime"></a>KSPROPERTY\_クロック\_PHYSICALTIME


クライアントの使用、KSPROPERTY\_クロック\_物理\_クロックの現在の物理的な時間を決定時のプロパティ。

## <span id="ddk_ksproperty_clock_physicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_PHYSICALTIME_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、100 ナノ秒単位の物理的な現在の時刻を表す LONGLONG 型の値を返します。

物理クロックの時刻は、これまで進行カウンターです。 プレゼンテーション時間とは異なり、取り消すことはできません。

クロックは、100 ナノ秒の解決をサポートする必要はありません。 クロックの解決策を決定するには、クライアントが使用できる、 [ **KSPROPERTY\_クロック\_解決**](ksproperty-clock-resolution.md)要求。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_クロック\_CORRELATEDPHYSICALTIME**](ksproperty-clock-correlatedphysicaltime.md)

[**KSPROPERTY\_クロック\_CORRELATEDTIME**](ksproperty-clock-correlatedtime.md)

 

 






