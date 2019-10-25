---
title: KSK プロパティ\_MEDIASEEKING\_期間
description: KSK プロパティ\_MEDIASEEKING\_DURATION プロパティは、フィルターのメディア期間を取得します。
ms.assetid: f84ff468-7cf6-4948-afee-a28ee365760d
keywords:
- KSPROPERTY_MEDIASEEKING_DURATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_DURATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394b6012de4a26530ac32086439a6d8ac5f64c95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842301"
---
# <a name="ksproperty_mediaseeking_duration"></a>KSK プロパティ\_MEDIASEEKING\_期間


KSK プロパティ\_MEDIASEEKING\_DURATION プロパティは、フィルターのメディア期間を取得します。

## <span id="ddk_ksproperty_mediaseeking_duration_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_DURATION_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、メディア期間を LONGLONG 型の値として返します。

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


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






