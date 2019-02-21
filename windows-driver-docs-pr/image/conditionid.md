---
title: ConditionId 要素
description: 必要な ConditionId 要素は、オフになっていたデバイスの条件を一意に識別します。
ms.assetid: 4b154fb3-625e-478d-9bb4-92fd7cae0530
keywords:
- ConditionId 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ConditionId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e49396c39e20c72640ae8d1be573bc0f6184856
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536501"
---
# <a name="conditionid-element"></a>ConditionId 要素


必要な**ConditionId**要素がオフになっていたデバイスの条件を一意に識別します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ConditionId>
  text
</wscn:ConditionId>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 以前に報告された DeviceCondition 要素の Id 属性に相当する整数値。

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
<td><p><a href="deviceconditioncleared.md" data-raw-source="[&lt;strong&gt;DeviceConditionCleared&lt;/strong&gt;](deviceconditioncleared.md)"><strong>DeviceConditionCleared</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ConditionId**要素である必要があります、 **Id**の属性を**DeviceCondition**要素の WSD スキャン サービスが以前に報告を[ **ScannerStatusConditionEvent**](scannerstatusconditionevent.md)します。

## <a name="see-also"></a>関連項目


[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






