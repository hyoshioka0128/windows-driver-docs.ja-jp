---
title: PlatenOpticalResolution 要素
description: 必須の PlatenOpticalResolution 要素は、最大の解像プラテンをスキャンできますを指定します。
ms.assetid: 770c204c-9315-47c6-afd3-4ac385e1177e
keywords:
- PlatenOpticalResolution 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PlatenOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe36297aa7e51605ec22e051d1af84dd00d0e7ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556652"
---
# <a name="platenopticalresolution-element"></a>PlatenOpticalResolution 要素


必要な**PlatenOpticalResolution**要素が最大の解像プラテンをスキャンできますを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PlatenOpticalResolution>
  child elements
</wscn:PlatenOpticalResolution>
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

として解像度が指定されて、 [**幅**](width.md) x [**高さ**](height.md)のペアを両方**幅**と**高さ**1 インチあたりのピクセル単位で指定されます。

高さの要素が指定されていない場合、WSD スキャン サービスは、正方形の画像の解像度を想定してください。 のみの場合など、**幅**100 の要素が提供される、解像度が 100 x 100 ピクセル/インチの四角形を前提としています。

## <a name="see-also"></a>関連項目


[**Height**](height.md)

[**プラテン**](platen.md)

[**幅**](width.md)

 

 






