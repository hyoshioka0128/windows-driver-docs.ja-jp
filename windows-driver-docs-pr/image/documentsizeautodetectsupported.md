---
title: DocumentSizeAutoDetectSupported 要素
description: 必要な DocumentSizeAutoDetectSupported 要素は、デバイスのスキャンが、元のメディアのサイズを検出できるかどうかを示します。
ms.assetid: 38baea3d-85bf-44e1-86bf-349d17981efa
keywords:
- DocumentSizeAutoDetectSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DocumentSizeAutoDetectSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec59f6f1847f0ce3653cc129d36956aeb1492070
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364508"
---
# <a name="documentsizeautodetectsupported-element"></a>DocumentSizeAutoDetectSupported 要素


必要な**DocumentSizeAutoDetectSupported**要素は、デバイスのスキャンが、元のメディアのサイズを検出できるかどうかを示します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DocumentSizeAutoDetectSupported>
  text
</wscn:DocumentSizeAutoDetectSupported>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 必要がありますは 0 を指定するブール値 false または true は 1 です。**falsetrue**

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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

デバイスのスキャンが、元のメディアのサイズを検出できる場合、WSD スキャン サービスは 1 を返す必要があります (**true**)、それ以外の 0 を返す必要があります (**false**)。

この要素に使用できる値を拡張することはできません。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

 

 






