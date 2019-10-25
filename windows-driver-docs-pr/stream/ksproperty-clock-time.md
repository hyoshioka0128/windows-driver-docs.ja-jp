---
title: KSK プロパティ\_CLOCK\_TIME
description: クライアントは、KSK プロパティ\_CLOCK\_TIME プロパティを使用して、クロックの現在のプレゼンテーション時刻を決定します。
ms.assetid: 42bae8fa-bff0-4411-bf32-5aa4da3e4f02
keywords:
- KSPROPERTY_CLOCK_TIME ストリーミングメディアデバイス
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
ms.openlocfilehash: d27b3dd2bc5ce8f22566b4eaf144e3d5a480565a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826856"
---
# <a name="ksproperty_clock_time"></a>KSK プロパティ\_CLOCK\_TIME


クライアントは、KSK プロパティ\_CLOCK\_TIME プロパティを使用して、クロックの現在のプレゼンテーション時刻を決定します。

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

このプロパティは、現在のプレゼンテーション時間を100ナノ秒単位で指定して、LONGLONG 型の値を返します。

クロックのプレゼンテーション時間は、物理的な時刻とは異なり、元に戻すことができます。 クロックのプレゼンテーション時間は、通常、基になるデータストリームのタイムスタンプを表します。 たとえば、DVD プレーヤーのクロックは、DVD 内の現在の位置のタイムスタンプをプレゼンテーション時間として報告できます。

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


[KSPROPSETID\_Clock](kspropsetid-clock.md)

 

 






