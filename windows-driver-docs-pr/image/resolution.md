---
title: 解決要素
description: 省略可能な解像度の要素には、スキャンした画像の解像度を指定します。
ms.assetid: d46c197d-40ed-4623-a842-7ee5cb9e8367
keywords:
- デバイスのイメージの解像度要素
topic_type:
- apiref
api_name:
- wscn Resolution wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255336081378ac86b22aeb48fdc150d1cc01089d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356234"
---
# <a name="resolution-element"></a>解決要素


省略可能な**解決**要素は、スキャンした画像の解像度を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Resolution wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Resolution wscn:MustHonor="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>幅</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**解像度**要素には、1 つが含まれています[**幅**](width.md) x [**高さ**](height.md)ペアについて説明しますが、。スキャンの解像度が必要です。 場合、**高さ**要素が見つからない、**幅**値を使用すると、正方形の解像度 (たとえば、300 x 300) を生成します。

**解像度**値は 1 インチあたりのピクセル単位。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、**解決**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**Height**](height.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**幅**](width.md)

 

 






