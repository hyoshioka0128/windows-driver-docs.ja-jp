---
title: KSPROPERTY\_MEDIASEEKING\_プリロール
description: KSPROPERTY\_MEDIASEEKING\_プリロール プロパティ フィルターに必要な 100 ナノ秒単位でプリロールの量を取得します。
ms.assetid: 3b9a5458-b26a-452b-b7aa-7bbb30c3d631
keywords:
- KSPROPERTY_MEDIASEEKING_PREROLL ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_PREROLL
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d563a91557e1ad7b242ec669c044bff816ebdede
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346494"
---
# <a name="kspropertymediaseekingpreroll"></a>KSPROPERTY\_MEDIASEEKING\_プリロール


KSPROPERTY\_MEDIASEEKING\_プリロール プロパティ フィルターに必要な 100 ナノ秒単位でプリロールの量を取得します。

## <span id="ddk_ksproperty_mediaseeking_preroll_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_PREROLL_KS"></span>


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
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、LONGLONG 型の値として、プリロールの 100 ナノ秒単位の数を返します。

<a name="requirements"></a>必要条件
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

 

 






