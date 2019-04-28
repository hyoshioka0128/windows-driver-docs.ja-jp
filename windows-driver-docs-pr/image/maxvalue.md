---
title: MaxValue 要素
description: 必須の MaxValue 要素には、値の範囲を必要とする構成要素をスキャナーのスキャン デバイスをサポートする最大値を指定します。
ms.assetid: a01833ff-06cd-47d3-9f54-2f1cf01cc1e6
keywords:
- MaxValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn MaxValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c858baf02a7c3920bb98213ac9575ff97bb20e3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380356"
---
# <a name="maxvalue-element"></a>MaxValue 要素


必要な**MaxValue**要素が値の範囲を必要とする構成要素をスキャナーのスキャン デバイスをサポートする最大値を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:MaxValue>
  text
</wscn:MaxValue>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 使用可能な値は、特定の親要素を参照してください。

## <a name="child-elements"></a>子要素


子要素はありません。

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
<td><p><a href="compressionqualityfactorsupported.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactorSupported&lt;/strong&gt;](compressionqualityfactorsupported.md)"><strong>CompressionQualityFactorSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scalingheight2.md" data-raw-source="[&lt;strong&gt;ScalingHeight&lt;/strong&gt;](scalingheight2.md)"><strong>ScalingHeight</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scalingwidth2.md" data-raw-source="[&lt;strong&gt;ScalingWidth&lt;/strong&gt;](scalingwidth2.md)"><strong>ScalingWidth</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

値、 **MaxValue**要素がその親要素に依存します。 有効な値では、適切な親要素を参照してください。

## <a name="see-also"></a>関連項目


[**CompressionQualityFactorSupported**](compressionqualityfactorsupported.md)

[**MinValue**](minvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingWidth**](scalingwidth2.md)

 

 






