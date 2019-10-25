---
title: KSK プロパティ\_CLOCK\_CORRELATEDTIME
description: クライアントは、KSK プロパティ\_CLOCK\_CORRELATEDTIME プロパティを使用して、クロックの現在のプレゼンテーション時刻を現在のシステム時刻と比較します。
ms.assetid: 12c377ec-b000-4256-8765-4da46208088d
keywords:
- KSPROPERTY_CLOCK_CORRELATEDTIME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_CORRELATEDTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac9d79beadb59c17f6a612e6954b478b3009242e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826902"
---
# <a name="ksproperty_clock_correlatedtime"></a>KSK プロパティ\_CLOCK\_CORRELATEDTIME


クライアントは、KSK プロパティ\_CLOCK\_CORRELATEDTIME プロパティを使用して、クロックの現在のプレゼンテーション時刻を現在のシステム時刻と比較します。

## <span id="ddk_ksproperty_clock_correlatedtime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_CORRELATEDTIME_KS"></span>


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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscorrelated_time" data-raw-source="[&lt;strong&gt;KSCORRELATED_TIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscorrelated_time)"><strong>KSCORRELATED_TIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

K焦げ RELATED\_TIME 構造体には、**時刻**メンバーの現在のクロック時間と**SystemTime**メンバーの関連する物理時間が含まれます。

「 [KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)」も参照してください。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_CLOCK\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

[**KeQueryPerformanceCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kequeryperformancecounter)

 

 






