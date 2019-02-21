---
title: RotationsSupported 要素
description: 必要な RotationsSupported 要素には、スキャナーをスキャンしたドキュメントの各イメージの回転をサポートする回転値の一覧が含まれています。
ms.assetid: da72cc1e-40e8-46a1-8215-0a20a52a0e19
keywords:
- RotationsSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn RotationsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5b0acfc05ace3e31b055f896f0c0461122350c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530266"
---
# <a name="rotationssupported-element"></a>RotationsSupported 要素


必要な**RotationsSupported**要素には、スキャナーをスキャンしたドキュメントの各イメージの回転をサポートする回転値の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:RotationsSupported>
  child elements
</wscn:RotationsSupported>
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
<td><p><a href="rotationvalue.md" data-raw-source="[&lt;strong&gt;RotationValue&lt;/strong&gt;](rotationvalue.md)"><strong>RotationValue</strong></a></p></td>
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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスは、データの取得後に、スキャン データにすべての回転値を適用する必要があります。 すべての回転は時計回り方向で適用する必要があります。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

[**RotationValue**](rotationvalue.md)

 

 






