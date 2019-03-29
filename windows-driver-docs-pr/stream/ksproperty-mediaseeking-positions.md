---
title: KSPROPERTY\_MEDIASEEKING\_位置
description: KSPROPERTY\_MEDIASEEKING\_POSITIONS プロパティ フィルターのメディア時間や停止時刻を設定します。
ms.assetid: 20f0e97a-37bb-4c01-8012-b73bb765f4b9
keywords:
- KSPROPERTY_MEDIASEEKING_POSITIONS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_POSITIONS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 288d877d6942183ae7fbdaead0ff4e24e09fc3ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571448"
---
# <a name="kspropertymediaseekingpositions"></a>KSPROPERTY\_MEDIASEEKING\_位置


KSPROPERTY\_MEDIASEEKING\_POSITIONS プロパティ フィルターのメディア時間や停止時刻を設定します。

## <span id="ddk_ksproperty_mediaseeking_positions_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_POSITIONS_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565207" data-raw-source="[&lt;strong&gt;KSPROPERTY_POSITIONS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565207)"><strong>KSPROPERTY_POSITIONS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KSPROPERTY\_構造体の指定、現在の位置を置き、ストリームの合計期間に対する相対的な位置を停止します。

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


[**KSPROPERTY\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff565207)

 

 






