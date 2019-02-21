---
title: RotationValue 要素
description: 必要な RotationValue 要素には、デバイスのスキャンでサポートされる 1 つの回転値を指定します。
ms.assetid: 89b8527a-309a-4344-bf6e-3155bb056acf
keywords:
- RotationValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn RotationValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b3a4fea4c1227e64da3185174f91789e0642e03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553660"
---
# <a name="rotationvalue-element"></a>RotationValue 要素


必要な**RotationValue**要素がデバイスのスキャンでサポートされる 1 つの回転値を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:RotationValue>
  text
</wscn:RotationValue>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 0、90、180、または 270 にする必要がある数値。

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
<td><p><a href="rotationssupported.md" data-raw-source="[&lt;strong&gt;RotationsSupported&lt;/strong&gt;](rotationssupported.md)"><strong>RotationsSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**RotationValue**要素は、スキャナーがスキャンしたドキュメントの各イメージを回転する角度の数値を指定します。 すべての回転は時計回り方向で適用されます。

すべての WSD スキャン サービスには、0 の値をサポートする必要があります。 両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**RotationsSupported**](rotationssupported.md)

 

 






