---
title: FilmResolutions 要素
description: 必要な FilmResolutions 要素には、入力ソースのスキャン、スキャナーのフィルムをスキャンできます解像度の一覧が含まれています。
ms.assetid: a273ac11-e1ae-4329-a6a2-e47accf564a9
keywords:
- FilmResolutions 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb24459bb3bd53047392984f96f786ac9cc2b13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559449"
---
# <a name="filmresolutions-element"></a>FilmResolutions 要素


必要な**FilmResolutions**要素には、入力ソースのスキャン、スキャナーのフィルムをスキャンできます解像度の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmResolutions>
  child elements
</wscn:FilmResolutions>
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>高さ</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="widths.md" data-raw-source="[&lt;strong&gt;Widths&lt;/strong&gt;](widths.md)"><strong>幅</strong></a></p></td>
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

として解像度が指定されて、 [**幅**](width.md) x [**高さ**](height.md)のペアを両方**幅**と**高さ**1 インチあたりのピクセル単位で指定されます。

WSD スキャン サービス内でスキャン デバイスをサポートするすべての設定可能な幅が一覧表示されます、**幅**子要素と内でスキャン デバイスをサポートするすべての可能な高さ、**高さ**子要素。 すべて**幅**と**高さ**値は、互いに依存しないと、ほとんどのデバイス サポート内の任意の組み合わせでペアになって、 [ **ScanTicket**](scanticket.md)要素。

## <a name="see-also"></a>関連項目


[**フィルム**](film.md)

[**Height**](height.md)

[**高さ**](heights.md)

[**ScanTicket**](scanticket.md)

[**幅**](width.md)

[**幅**](widths.md)

 

 






