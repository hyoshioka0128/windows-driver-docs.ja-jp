---
title: 要素の高さ
description: 必要な高さ要素には、スキャナーが画像をスキャンする高さの一覧が含まれています。
ms.assetid: b45a967e-9ce9-417a-96f2-c199ab302b88
keywords:
- デバイスのイメージの高さ要素
topic_type:
- apiref
api_name:
- wscn Heights
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b7ad6b8a7e165a71a3e70dfc041afb756ba676
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330275"
---
# <a name="heights-element"></a>要素の高さ


必要な**高さ**要素には、スキャナーが画像をスキャンする高さの一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Heights>
  child elements
</wscn:Heights>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
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

各[**高さ**](height.md)子要素が垂直方向の位置は、デバイスが画像をスキャンできます 1 インチあたりのピクセルの有効な数値を指定します。

[**幅**](widths.md)要素には、スキャナーをサポートする幅のリストが含まれています。

## <a name="see-also"></a>関連項目


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**Height**](height.md)

[**PlatenResolutions**](platenresolutions.md)

[**幅**](width.md)

[**幅**](widths.md)

 

 






