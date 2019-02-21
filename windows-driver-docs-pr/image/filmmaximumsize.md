---
title: FilmMaximumSize 要素
description: 必要な FilmMaximumSize 要素には、エンドユーザーが入力ソースをスキャンするフィルムをスキャンできる最大サイズ元を指定します。
ms.assetid: 936c3c4e-5b09-433e-876c-9eda438dde9c
keywords:
- FilmMaximumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4143b4b16c12c56bd6ded7a75bf2fa98248886c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560928"
---
# <a name="filmmaximumsize-element"></a>FilmMaximumSize 要素


必要な**FilmMaximumSize**要素は、エンドユーザーが入力ソースをスキャンするフィルムをスキャンできる最大サイズ元を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmMaximumSize>
  child elements
</wscn:FilmMaximumSize>
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>フィルム</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

[**幅**](width.md)子要素が入力ソースをスキャンするフィルムを高速スキャン方向でサポートするメディアの最大サイズを指定します。 [**高さ**](height.md)子要素が入力ソースをスキャンするフィルムが低速スキャン方向でサポートしているメディアの最大サイズを指定します。

メディアのすべてのディメンションが 1 つの部分の 1/1000 で測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**フィルム**](film.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






