---
title: ScalingHeight 要素
description: 必要な ScalingHeight 要素には、出力ドキュメントの高さを拡大縮小に使用できる値の範囲が含まれています。
ms.assetid: f13e1ef8-e05f-4aab-bf2a-08a953638334
keywords:
- ScalingHeight 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScalingHeight
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad54a20b497e2fed139a5a0c78af2f681c468a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364395"
---
# <a name="scalingheight-element"></a>ScalingHeight 要素


必要な**ScalingHeight**要素には、出力ドキュメントの高さを拡大縮小に使用できる値の範囲が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScalingHeight>
  child elements
</wscn:ScalingHeight>
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
<td><p><a href="maxvalue.md" data-raw-source="[&lt;strong&gt;MaxValue&lt;/strong&gt;](maxvalue.md)"><strong>MaxValue</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="minvalue.md" data-raw-source="[&lt;strong&gt;MinValue&lt;/strong&gt;](minvalue.md)"><strong>MinValue</strong></a></p></td>
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
<td><p><a href="scalingrangesupported.md" data-raw-source="[&lt;strong&gt;ScalingRangeSupported&lt;/strong&gt;](scalingrangesupported.md)"><strong>ScalingRangeSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ScalingHeight**要素が含まれています、 [ **MinValue** ](minvalue.md)と[ **MaxValue** ](maxvalue.md)要素です出力ドキュメントの高さを拡張するため、デバイスのスキャンをサポートする最小値と最大値を指定します。

**MinValue**と**MaxValue**と 1 ~ 1000 の整数でなければなりません**MinValue**に等しいまたはそれよりも小さい**MaxValue**します。 100 にすると、デバイスのスキャンは、スキャンしたイメージの高さに調整をしないでの値。 少なくとも、WSD スキャン サービスは、100 の値をサポートする必要があります。

## <a name="see-also"></a>関連項目


[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScalingWidth2**](scalingwidth.md)

 

 






