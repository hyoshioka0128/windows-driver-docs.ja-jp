---
title: ContrastSupported 要素
description: 必要な ContrastSupported 要素では、デバイスのスキャンがスキャン コントラストの設定のユーザーによる制御をサポートしているかどうかを指定します。
ms.assetid: 9b865f9f-b5f6-4bb3-9f24-3df896845e96
keywords:
- ContrastSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ContrastSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7296dc177769fd80357de7a705ab2ed587c64375
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577701"
---
# <a name="contrastsupported-element"></a>ContrastSupported 要素


必要な**ContrastSupported**要素は、デバイスのスキャンがスキャン コントラストの設定のユーザーによる制御をサポートしているかどうかを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ContrastSupported>
  text
</wscn:ContrastSupported>
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

<a name="remarks"></a>コメント
-------

デバイスのスキャンは、スキャンのコントラスト設定のユーザーによる制御を許可している場合、WSD スキャン サービスは 1 を返す必要があります (**true**)、それ以外の 0 を返す必要があります (**false**)。

この要素に使用できる値を拡張することはできません。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

 

 






