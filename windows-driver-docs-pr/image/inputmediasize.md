---
title: InputMediaSize 要素
description: 必要な InputMediaSize 要素には、現在のジョブをスキャンするメディアのサイズを指定します。
ms.assetid: f1fcb152-96c5-469c-8989-a2c4328a5f68
keywords:
- InputMediaSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn InputMediaSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b80a5c97766d360dafd2670c78cef7bf4418198
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360052"
---
# <a name="inputmediasize-element"></a>InputMediaSize 要素


必要な**InputMediaSize**要素を現在のジョブをスキャンするメディアのサイズを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:InputMediaSize>
  child elements
</wscn:InputMediaSize>
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
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**InputMediaSize**要素が含まれています、幅と、スキャンする入力メディアの高さで指定された、 [**幅**](width.md)と[**高さ** ](height.md)要素では、それぞれします。

**幅**要素には、高速スキャンの方向に元のメディアの幅が含まれています。 および**高さ**要素には、低速スキャン方向で、元のメディアの高さが含まれています。 両方**幅**と**高さ**1 1/10、1/100、1/1000 の単位で、1 ~ 2147483648 範囲内で指定する必要があります (1/1000) インチです。

## <a name="see-also"></a>関連項目


[**Height**](height.md)

[**InputSize**](inputsize.md)

[**幅**](width.md)

 

 






