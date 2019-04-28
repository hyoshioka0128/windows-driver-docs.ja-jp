---
title: PlatenResolutions 要素
description: 必要な PlatenResolutions 要素には、スキャナーのプラテンをスキャンできます解像度の一覧が含まれています。
ms.assetid: 9adf54d7-4cca-4d43-b467-c0b2c84a4a7f
keywords:
- PlatenResolutions 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PlatenResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a70e40e26d8475d4b6631e6fb2e76dc2f44f45d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360641"
---
# <a name="platenresolutions-element"></a>PlatenResolutions 要素


必要な**PlatenResolutions**要素には、スキャナーのプラテンをスキャンできます解像度の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PlatenResolutions>
  child elements
</wscn:PlatenResolutions>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>プラテン</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

として解像度が指定されて、 [**幅**](width.md) x [**高さ**](height.md)ペア、幅と高さの両方が 1 インチあたりのピクセル単位で指定されています。

WSD スキャン サービスは、幅の子要素内でスキャン デバイスをサポートするすべての設定可能な幅と高さの子要素内でスキャン デバイスをサポートするすべての可能な高さに一覧表示する必要があります。 すべての幅と高さの値は、互いに依存しないと、ほとんどのデバイス サポート内の任意の組み合わせでペアになって、 [ **ScanTicket** ](scanticket.md)要素。

## <a name="see-also"></a>関連項目


[**Height**](height.md)

[**高さ**](heights.md)

[**プラテン**](platen.md)

[**ScanTicket**](scanticket.md)

[**幅**](width.md)

[**幅**](widths.md)

 

 






