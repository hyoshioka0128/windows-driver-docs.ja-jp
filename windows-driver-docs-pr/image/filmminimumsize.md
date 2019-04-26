---
title: FilmMinimumSize 要素
description: 必要な FilmMinimumSize 要素には、エンドユーザーがスキャン オプション フィルムをスキャンできる最小サイズ元を指定します。
ms.assetid: bce03ce1-9f2f-489f-ae71-a81474895410
keywords:
- FilmMinimumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8251ec82e9558d267650015007ea6815393487ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354618"
---
# <a name="filmminimumsize-element"></a>FilmMinimumSize 要素


必要な**FilmMinimumSize**要素は、エンドユーザーがスキャン オプション フィルムをスキャンできる最小サイズ元を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmMinimumSize>
  child elements
</wscn:FilmMinimumSize>
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

[**幅**](width.md)子要素が入力ソースをスキャンするフィルムを高速スキャン方向でサポートするメディアの最小サイズを指定します。 [**高さ**](height.md)子要素が入力ソースをスキャンするフィルムが低速スキャン方向でサポートしているメディアの最小サイズを指定します。

メディアのすべてのディメンションが 1 つの部分の 1/1000 で測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**フィルム**](film.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






