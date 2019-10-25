---
title: KSK プロパティ\_CLOCK\_PHYSICALTIME
description: クライアントは、KSK プロパティ\_CLOCK\_物理\_時間プロパティを使用して、クロックの現在の時刻を決定します。
ms.assetid: cc747fd4-1df0-4d44-b43e-b43532c1228b
keywords:
- KSPROPERTY_CLOCK_PHYSICALTIME ストリーミングメディアデバイス
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
ms.openlocfilehash: 5e30a1223af128759016de98b7262f53644021dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826898"
---
# <a name="ksproperty_clock_physicaltime"></a>KSK プロパティ\_CLOCK\_PHYSICALTIME


クライアントは、KSK プロパティ\_CLOCK\_物理\_時間プロパティを使用して、クロックの現在の時刻を決定します。

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
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、現在の物理時刻を100ナノ秒単位で表す、LONGLONG 型の値を返します。

クロックの物理的な時刻は、常に進行中のカウンターです。 プレゼンテーション時間とは異なり、反転することはできません。

クロックは、100ナノ秒の解像度をサポートするためには必要ありません。 クロックの解像度を決定するために、クライアントは、 [**Ksk プロパティ\_clock\_resolution**](ksproperty-clock-resolution.md)要求を使用できます。

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


[**KSK プロパティ\_CLOCK\_CORRELATEDPHYSICALTIME**](ksproperty-clock-correlatedphysicaltime.md)

[**KSK プロパティ\_CLOCK\_CORRELATEDTIME**](ksproperty-clock-correlatedtime.md)

 

 






