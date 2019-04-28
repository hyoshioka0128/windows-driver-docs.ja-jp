---
title: KSPROPERTY\_MEDIASEEKING\_書式設定
description: KSPROPERTY\_MEDIASEEKING\_形式のプロパティを取得しますメディア時間フィルターでサポートされる形式。 この情報は、複数の項目のプロパティとして返されます。
ms.assetid: 6d01737e-baef-4a65-90c7-3838cb19b4c9
keywords:
- KSPROPERTY_MEDIASEEKING_FORMATS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_FORMATS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d61fcc4b98f8a7a4e595abd4906a23061ebbd52d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366100"
---
# <a name="kspropertymediaseekingformats"></a>KSPROPERTY\_MEDIASEEKING\_書式設定


KSPROPERTY\_MEDIASEEKING\_形式のプロパティを取得しますメディア時間フィルターでサポートされる形式。 この情報は、複数の項目のプロパティとして返されます。

## <span id="ddk_ksproperty_mediaseeking_formats_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_FORMATS_KS"></span>


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
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、複数の項目のプロパティを返すことができます。 依頼者は、適切なサイズのバッファーを提供する責任を負います。

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


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






