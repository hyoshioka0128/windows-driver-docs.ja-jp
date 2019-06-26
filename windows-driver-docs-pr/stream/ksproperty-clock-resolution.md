---
title: KSPROPERTY\_クロック\_解決
description: クライアントの使用、KSPROPERTY\_クロック\_クロックの有効桁数を決定するプロパティを解決します。
ms.assetid: 3e92a4fb-207f-449a-bc70-aa8028b4f8f1
keywords:
- KSPROPERTY_CLOCK_RESOLUTION ストリーミング メディア デバイス
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
ms.openlocfilehash: 39e8c72b99cc9c13d0f1628d0021641365a4ea4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373142"
---
# <a name="kspropertyclockresolution"></a>KSPROPERTY\_クロック\_解決


クライアントの使用、KSPROPERTY\_クロック\_クロックの有効桁数を決定するプロパティを解決します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksresolution" data-raw-source="[&lt;strong&gt;KSRESOLUTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksresolution)"><strong>KSRESOLUTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

導入された、遅延、**エラー**メンバーはまた、**粒度**メンバー。 クロックなど、**粒度**のいずれかと**エラー** 2 つのことになりますすべて 300 ナノ秒クロック イベント通知を発行します。

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


[**KSCLOCK\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksclock_dispatch)

[**KSRESOLUTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksresolution)

[**KSPROPERTY\_クロック\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

 

 






