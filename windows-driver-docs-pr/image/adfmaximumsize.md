---
title: ADFMaximumSize 要素
description: 必要な ADFMaximumSize 要素は、自動ドキュメント フィーダー (ADF) の前または後ろにある、エンドユーザーがスキャンできる最大サイズのドキュメントを指定します。
ms.assetid: 8304bbae-e0ed-40f3-b3aa-2a818664b76a
keywords:
- ADFMaximumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8658597ae5544635a8515c68b9398d61f516ef86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529036"
---
# <a name="adfmaximumsize-element"></a>ADFMaximumSize 要素


必要な**ADFMaximumSize**自動ドキュメント フィーダー (ADF) の前または後ろにある要素が、エンドユーザーがスキャンできる最大サイズのドキュメントを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFMaximumSize>
  child elements
</wscn:ADFMaximumSize>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

[**幅**](width.md)子要素は、ADF を高速スキャン方向でサポートするメディアの最大サイズを指定します。 [**高さ**](height.md)子要素は、ADF が低速スキャン方向でサポートしているメディアの最大サイズを指定します。

場合の親要素、 **ADFMaximumSize**要素は[ **ADFFront**](adffront.md)、指定された最大サイズは、ADF の正面に適用されますそれ以外の場合、親要素は、。[ **ADFBack** ](adfback.md)と最大サイズは、ADF の背面に適用されます。

メディアのすべてのディメンションが 1 つの部分の 1/1000 で測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






