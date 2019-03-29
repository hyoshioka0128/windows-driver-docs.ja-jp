---
title: KSPROPERTY\_クロスバー\_できます\_ルート
description: KSPROPERTY\_クロスバー\_できます\_ルート プロパティは、デバイスが、指定したルーティングをサポートできるかどうかを取得します。 このプロパティを実装する必要があります。
ms.assetid: bb966d0a-6ecf-4bbb-a881-30d468abe220
keywords:
- KSPROPERTY_CROSSBAR_CAN_ROUTE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_CAN_ROUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f8b6777851c8b3f96897b72224c40cc3c03019
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573332"
---
# <a name="kspropertycrossbarcanroute"></a>KSPROPERTY\_クロスバー\_できます\_ルート


KSPROPERTY\_クロスバー\_できます\_ルート プロパティは、デバイスが、指定したルーティングをサポートできるかどうかを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_crossbar_can_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAN_ROUTE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ストリーミングのミニドライバーが 2 つの pin の間で指定したルーティングをサポートしているかどうかを指定する ULONG。 0 以外の値は、ルーティングがサポートされていることを示します。 ミニドライバーは、2 つの pin の間のルーティングをサポートしていません、この値は 0 です。

<a name="remarks"></a>コメント
-------

**CanRoute** 、KSPROPERTY のメンバー\_クロスバー\_ルート\_の構造は、デバイスが、指定したルーティングをサポートできることを示します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_クロスバー\_ルート\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565128)

 

 






