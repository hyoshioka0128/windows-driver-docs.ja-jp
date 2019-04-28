---
title: 要素の幅
description: 必要な幅要素には、スキャナーが画像をスキャンする幅のリストが含まれています。
ms.assetid: 785d469f-bdad-413c-8bfb-de7a518b243c
keywords:
- デバイスのイメージの幅要素
topic_type:
- apiref
api_name:
- wscn Widths
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ff2d7262c2c30be8827726630c83e8f4fdd0afe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380230"
---
# <a name="widths-element"></a>要素の幅


必要な**幅**要素には、スキャナーが画像をスキャンする幅のリストが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Widths>
  child elements
</wscn:Widths>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><a href="adfresolutions.md" data-raw-source="[&lt;strong&gt;ADFResolutions&lt;/strong&gt;](adfresolutions.md)"><strong>ADFResolutions</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmresolutions.md" data-raw-source="[&lt;strong&gt;FilmResolutions&lt;/strong&gt;](filmresolutions.md)"><strong>FilmResolutions</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenresolutions.md" data-raw-source="[&lt;strong&gt;PlatenResolutions&lt;/strong&gt;](platenresolutions.md)"><strong>PlatenResolutions</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

各[**幅**](width.md)子要素を水平方向の位置は、デバイスが画像をスキャンできます 1 インチあたりのピクセルの有効な数値を指定します。

[**高さ**](heights.md)要素には、スキャナーをサポートする高さの一覧が含まれています。

## <a name="see-also"></a>関連項目


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**Height**](height.md)

[**高さ**](heights.md)

[**PlatenResolutions**](platenresolutions.md)

[**幅**](width.md)

 

 






