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
ms.openlocfilehash: 0d9ac1f25cbcda65fdcc167111b97fa5a80e2da6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528224"
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
<td><p>X</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566806" data-raw-source="[&lt;strong&gt;KSRESOLUTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566806)"><strong>KSRESOLUTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

導入された、遅延、**エラー**メンバーはまた、**粒度**メンバー。 クロックなど、**粒度**のいずれかと**エラー** 2 つのことになりますすべて 300 ナノ秒クロック イベント通知を発行します。

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


[**KSCLOCK\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff561017)

[**KSRESOLUTION**](https://msdn.microsoft.com/library/windows/hardware/ff566806)

[**KSPROPERTY\_クロック\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

 

 






