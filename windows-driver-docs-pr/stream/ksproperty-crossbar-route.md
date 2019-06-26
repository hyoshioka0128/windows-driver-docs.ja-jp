---
title: KSPROPERTY\_クロスバー\_ルート
description: KSPROPERTY\_クロスバー\_ルート プロパティ クエリを実行して、特定のルーティングが可能かどうか、出力ピン留めするインデックスと、入力ピン インデックスを指定することでビデオまたはオーディオのストリームをルーティングします。 このプロパティを実装する必要があります。
ms.assetid: 2c64575c-49c6-437b-924e-042ee0f15d9b
keywords:
- KSPROPERTY_CROSSBAR_ROUTE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_ROUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d1f1b43c65929461d15656ad4641b309f0f3122
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373080"
---
# <a name="kspropertycrossbarroute"></a>KSPROPERTY\_クロスバー\_ルート


KSPROPERTY\_クロスバー\_ルート プロパティ クエリを実行して、特定のルーティングが可能かどうか、出力ピン留めするインデックスと、入力ピン インデックスを指定することでビデオまたはオーディオのストリームをルーティングします。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_crossbar_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_ROUTE_KS"></span>


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
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_クロス\_ルート\_特定のルーティングとルーティングが可能かどうかを指定する構造。

<a name="remarks"></a>注釈
-------

オーディオ出力ピンが出力オーディオ ストリームの場合などにミュートする-1 のインデックスの入力ピンにルーティングされると、ときに、チャネルを変更します。

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

 

 






