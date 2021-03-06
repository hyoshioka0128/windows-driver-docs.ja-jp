---
title: KSPROPERTY\_クロック\_CORRELATEDPHYSICALTIME
description: クライアントの使用、KSPROPERTY\_クロック\_CORRELATEDPHYSICALTIME プロパティを現在のシステム時刻のクロックの現在の物理的な時刻を比較します。
ms.assetid: 49f74411-1489-4864-9213-e1894128e355
keywords:
- KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3250b9b3e2fa6de53ce4fe6b80d6e1f57e192a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373151"
---
# <a name="kspropertyclockcorrelatedphysicaltime"></a>KSPROPERTY\_クロック\_CORRELATEDPHYSICALTIME


クライアントの使用、KSPROPERTY\_クロック\_CORRELATEDPHYSICALTIME プロパティを現在のシステム時刻のクロックの現在の物理的な時刻を比較します。

## <span id="ddk_ksproperty_clock_correlatedphysicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscorrelated_time" data-raw-source="[&lt;strong&gt;KSCORRELATED_TIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscorrelated_time)"><strong>KSCORRELATED_TIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSCORRELATED\_時間構造体には現在のクロック時間が含まれています、**時間**メンバーとの相関関係を持つ物理時刻、 **SystemTime**メンバー。

参照してください[KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)します。

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


[**KSPROPERTY\_クロック\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

[**KeQueryPerformanceCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kequeryperformancecounter)

 

 






