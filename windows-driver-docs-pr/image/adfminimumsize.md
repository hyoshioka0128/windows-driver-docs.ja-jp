---
title: ADFMinimumSize 要素
description: 必須の ADFMinimumSize 要素は、前面または背面 (ADF) の自動ドキュメント フィーダーにエンドユーザーがスキャンできる最小サイズ元を指定します。
ms.assetid: 9304bb42-8ec4-4e79-95ce-af2aed4a58e2
keywords:
- ADFMinimumSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41758405f7a3c813a33f504762760424f7bc918
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367070"
---
# <a name="adfminimumsize-element"></a>ADFMinimumSize 要素


必要な**ADFMinimumSize**前面または背面 (ADF) の自動ドキュメント フィーダー要素は、エンドユーザーがスキャンできる最小サイズ元を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFMinimumSize>
  child elements
</wscn:ADFMinimumSize>
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

[**幅**](width.md)子要素は、ADF を高速スキャン方向でサポートするメディアの最小サイズを指定します。 [**高さ**](height.md)子要素は、ADF が低速スキャン方向でサポートしているメディアの最小サイズを指定します。

場合の親要素、 **ADFMinimumSize**要素は[ **ADFFront**](adffront.md)、指定したサイズは、ADF の正面に適用されますそれ以外の親要素は。[**ADFBack** ](adfback.md)サイズは、ADF の背面に適用されます。

メディアのすべてのディメンションが 1 つの桁区切りで測定されます (1/1000) インチです。 両方で使用できる値**幅**と**高さ**1 ~ 2147483648 範囲。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






