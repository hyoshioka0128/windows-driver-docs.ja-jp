---
title: MinValue 要素
description: 必須の MinValue 要素には、値の範囲を必要とする構成要素をスキャナーのスキャン デバイスをサポートする最小値を指定します。
ms.assetid: ea20d077-bf2d-42a1-8dba-69e8aaf2881c
keywords:
- MinValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn MinValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0446201792f813173f18a91270e3dd3da820ed08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379680"
---
# <a name="minvalue-element"></a>MinValue 要素


必要な**MinValue**要素が値の範囲を必要とする構成要素をスキャナーのスキャン デバイスをサポートする最小値を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:MinValue>
  text
</wscn:MinValue>
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

値、 **MinValue**要素がその親要素に依存します。 有効な値では、適切な親要素を参照してください。

## <a name="see-also"></a>関連項目


[**CompressionQualityFactorSupported**](compressionqualityfactorsupported.md)

[**MaxValue**](maxvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingWidth**](scalingwidth2.md)

 

 






