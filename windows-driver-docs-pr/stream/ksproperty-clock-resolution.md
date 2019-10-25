---
title: KSK プロパティ\_クロック\_解像度
description: クライアントは、KSK プロパティ\_CLOCK\_RESOLUTION プロパティを使用して、クロックの有効桁数を決定します。
ms.assetid: 3e92a4fb-207f-449a-bc70-aa8028b4f8f1
keywords:
- KSPROPERTY_CLOCK_RESOLUTION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_RESOLUTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acf368ffa5feade4c5dc9c39ed44137a33971cd2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826894"
---
# <a name="ksproperty_clock_resolution"></a>KSK プロパティ\_クロック\_解像度


クライアントは、KSK プロパティ\_CLOCK\_RESOLUTION プロパティを使用して、クロックの有効桁数を決定します。

## <span id="ddk_ksproperty_clock_resolution_ks"></span><span id="DDK_KSPROPERTY_CLOCK_RESOLUTION_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution" data-raw-source="[&lt;strong&gt;KSRESOLUTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution)"><strong>KSRESOLUTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**エラー**メンバーで導入された遅延は、**粒度**メンバーに含まれています。 たとえば、**粒度**が1で**エラー**が2のクロックは、300ナノ秒ごとにクロックイベント通知を発行することができます。

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


[**KSCLOCK\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksclock_dispatch)

[**KSRESOLUTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution)

[**KSK プロパティ\_CLOCK\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

 

 






