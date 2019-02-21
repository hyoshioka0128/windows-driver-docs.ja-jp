---
title: PlatenMinimumSize 要素
description: 必要な PlatenMinimumSize 要素では、ベッドからプラテン上、エンドユーザーがスキャンできる最小サイズのドキュメントを指定します。
ms.assetid: 8db5092f-415c-4942-a4a7-733a381afd16
keywords:
- PlatenMinimumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PlatenMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64120f6376fecb2cb864e41b6c0a901f00e56d88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557810"
---
# <a name="platenminimumsize-element"></a>PlatenMinimumSize 要素


必要な**PlatenMinimumSize**要素は、フラット ベッドからプラテン上でエンドユーザーがスキャンできる最小サイズのドキュメントを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PlatenMinimumSize>
  child elements
</wscn:PlatenMinimumSize>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>プラテン</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

[**幅**](width.md)子要素からプラテン上を高速スキャン方向でサポートするメディアの最小サイズを指定します。 [**高さ**](height.md)子要素が低速スキャン方向からプラテン上をサポートするメディアの最小サイズを指定します。

メディアのすべてのディメンションが 1 つの部分の 1/1000 で測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**Height**](height.md)

[**プラテン**](platen.md)

[**幅**](width.md)

 

 






