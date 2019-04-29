---
title: KSPROPERTY\_クロック\_時間
description: クライアントの使用、KSPROPERTY\_クロック\_時間プロパティのクロックの現在のプレゼンテーション時間。
ms.assetid: 42bae8fa-bff0-4411-bf32-5aa4da3e4f02
keywords:
- KSPROPERTY_CLOCK_TIME ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_TIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd165c7c7364cb0c822790f637e0df67927495d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330286"
---
# <a name="kspropertyclocktime"></a>KSPROPERTY\_クロック\_時間


クライアントの使用、KSPROPERTY\_クロック\_時間プロパティのクロックの現在のプレゼンテーション時間。

## <span id="ddk_ksproperty_clock_time_ks"></span><span id="DDK_KSPROPERTY_CLOCK_TIME_KS"></span>


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

このプロパティは、100 ナノ秒単位で現在のプレゼンテーション時間を指定する LONGLONG 型の値を返します。

物理的な時間とは異なり、クロックのプレゼンテーション時間を切り替えることができます。 クロックのプレゼンテーション時間は、通常、基になるデータ ストリームのタイムスタンプを表します。 たとえば、DVD プレーヤーのクロックは、プレゼンテーション時間として、DVD 内の現在位置のタイムスタンプを報告できます。

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


[KSPROPSETID\_クロック](kspropsetid-clock.md)

 

 






