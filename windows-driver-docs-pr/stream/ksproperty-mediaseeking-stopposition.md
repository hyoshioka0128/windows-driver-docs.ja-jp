---
title: KSPROPERTY\_MEDIASEEKING\_STOPPOSITION
description: KSPROPERTY\_MEDIASEEKING\_STOPPOSITION プロパティ フィルターの停止のメディア時間を取得します。
ms.assetid: 5a2d6c47-8419-4f1d-a362-28bf17cbd0a5
keywords:
- KSPROPERTY_MEDIASEEKING_STOPPOSITION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_STOPPOSITION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa3a5dae3fa1cac0a04656545c5a5510d2dbef2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580091"
---
# <a name="kspropertymediaseekingstopposition"></a>KSPROPERTY\_MEDIASEEKING\_STOPPOSITION


KSPROPERTY\_MEDIASEEKING\_STOPPOSITION プロパティ フィルターの停止のメディア時間を取得します。

## <span id="ddk_ksproperty_mediaseeking_stopposition_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_STOPPOSITION_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

停止のメディア時間は、停止時刻がフィルターでサポートされている場合に設定可能な時間です。

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

 

 






