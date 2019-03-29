---
title: MediaBack 要素
description: 省略可能な MediaBack 要素には、物理メディアの背面のスキャンに固有のすべてのパラメーターが含まれています。
ms.assetid: d736c76f-7ea7-49ca-9ad9-df35924fc7b4
keywords:
- MediaBack 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn MediaBack
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e149509b47163193ad9e2f3bd10d08eb69f78b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574346"
---
# <a name="mediaback-element"></a>MediaBack 要素


省略可能な**MediaBack**要素には、物理メディアの背面のスキャンに固有のすべてのパラメーターが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:MediaBack>
  child elements
</wscn:MediaBack>
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
<td><p><a href="colorprocessing.md" data-raw-source="[&lt;strong&gt;ColorProcessing&lt;/strong&gt;](colorprocessing.md)"><strong>ColorProcessing</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="resolution.md" data-raw-source="[&lt;strong&gt;Resolution&lt;/strong&gt;](resolution.md)"><strong>解決方法</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanregion.md" data-raw-source="[&lt;strong&gt;ScanRegion&lt;/strong&gt;](scanregion.md)"><strong>ScanRegion</strong></a></p></td>
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
<td><p><a href="mediasides.md" data-raw-source="[&lt;strong&gt;MediaSides&lt;/strong&gt;](mediasides.md)"><strong>MediaSides</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

**MediaBack**要素が無効にすると、スキャナーとのみをサポート双方向のスキャンで定義されている現在の入力ソース、 [**指定**](inputsource.md)要素は**ADFDuplex**します。

場合、 **MediaBack**要素が含まれていない、 [ **ScanRegion** ](scanregion.md)要素、WSD スキャン サービスが使用 0 オフセットおよび幅と高さのとして、 [**InputMediaSize**](inputmediasize.md)、指定した場合。 場合**ScanRegion**がないと**InputMediaSize**が指定されていないかによって判断できないデバイスのスキャン、実装を指定できます。

入力ソースがある場合**ADFDuplex**と**MediaBack**要素がありません、すべてのパラメーターで指定されている[ **MediaFront** ](mediafront.md)されますスキャンも背面に適用されます。

## <a name="see-also"></a>関連項目


[**ColorProcessing**](colorprocessing.md)

[**InputMediaSize**](inputmediasize.md)

[**指定**](inputsource.md)

[**MediaFront**](mediafront.md)

[**MediaSides**](mediasides.md)

[**解決方法**](resolution.md)

[**ScanRegion**](scanregion.md)

 

 






