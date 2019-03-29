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
ms.openlocfilehash: e56749a9cacf713128189b15603e97b6b3e6fba1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580922"
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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_クロス\_ルート\_特定のルーティングとルーティングが可能かどうかを指定する構造。

<a name="remarks"></a>コメント
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

[**KSPROPERTY\_クロスバー\_ルート\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565128)

 

 






