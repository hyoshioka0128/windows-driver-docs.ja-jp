---
title: BrightnessSupported 要素
description: 必要な BrightnessSupported 要素では、デバイスのスキャンがスキャン明るさの設定のユーザーによる制御をサポートしているかどうかを指定します。
ms.assetid: aa0eb627-694f-45a1-a923-07fc04b0612b
keywords:
- BrightnessSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn BrightnessSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 100c4d35c4eb69b1ecb30014d309ef306e24bb36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535889"
---
# <a name="brightnesssupported-element"></a>BrightnessSupported 要素


必要な**BrightnessSupported**要素は、デバイスのスキャンがスキャン明るさの設定のユーザーによる制御をサポートしているかどうかを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:BrightnessSupported>
  text
</wscn:BrightnessSupported>
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

デバイスのスキャンは、スキャンの明るさの設定のユーザーによる制御を許可している場合、WSD スキャン サービスは 1 を返す必要があります (**true**)、それ以外の 0 を返す必要があります (**false**)。

この要素に使用できる値を拡張することはできません。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

 

 






