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
ms.openlocfilehash: 07c7131899b9fa3e8e800ae4bf9f9214790b8aea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373098"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ストリーミングのミニドライバーが 2 つの pin の間で指定したルーティングをサポートしているかどうかを指定する ULONG。 0 以外の値は、ルーティングがサポートされていることを示します。 ミニドライバーは、2 つの pin の間のルーティングをサポートしていません、この値は 0 です。

<a name="remarks"></a>注釈
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

[**KSPROPERTY\_クロスバー\_ルート\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)

 

 






