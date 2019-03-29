---
title: PlatenMaximumSize 要素
description: 必要な PlatenMaximumSize 要素では、ベッドからプラテン上、エンドユーザーがスキャンできる最大サイズのドキュメントを指定します。
ms.assetid: dedeb5cf-588f-48dd-aea9-78c2a17f19e6
keywords:
- PlatenMaximumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PlatenMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545ced2e7d34f34b289c0382172b91775334585d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579042"
---
# <a name="platenmaximumsize-element"></a>PlatenMaximumSize 要素


必要な**PlatenMaximumSize**要素は、フラット ベッドからプラテン上でエンドユーザーがスキャンできる最大サイズのドキュメントを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PlatenMaximumSize>
  child elements
</wscn:PlatenMaximumSize>
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

<a name="remarks"></a>コメント
-------

[**幅**](width.md)子要素からプラテン上を高速スキャン方向でサポートするメディアの最大サイズを指定します。 [**高さ**](height.md)子要素が低速スキャン方向からプラテン上をサポートするメディアの最大サイズを指定します。

メディアのすべてのディメンションが 1 つの部分の 1/1000 で測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**Height**](height.md)

[**プラテン**](platen.md)

[**幅**](width.md)

 

 






