---
title: DeviceConditionCleared 要素
description: 必要な DeviceConditionCleared 要素がクリアされて以前に報告された DeviceCondition 状態に関する情報が含まれています。
ms.assetid: f4ed3d25-cee0-4532-84aa-d1cdd144ce2a
keywords:
- DeviceConditionCleared 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DeviceConditionCleared
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2aab29ddeb8ee49430928f2b4f81dbc8a7c12fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529999"
---
# <a name="deviceconditioncleared-element"></a>DeviceConditionCleared 要素


必要な**DeviceConditionCleared**要素には、以前のレポートに関する情報が含まれています。 [ **DeviceCondition** ](devicecondition.md)がクリアされた条件。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DeviceConditionCleared>
  child elements
</wscn:DeviceConditionCleared>
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
<td><p><a href="conditioncleartime.md" data-raw-source="[&lt;strong&gt;ConditionClearTime&lt;/strong&gt;](conditioncleartime.md)"><strong>ConditionClearTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="conditionid.md" data-raw-source="[&lt;strong&gt;ConditionId&lt;/strong&gt;](conditionid.md)"><strong>ConditionId</strong></a></p></td>
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
<td><p><a href="scannerstatusconditionevent.md" data-raw-source="[&lt;strong&gt;ScannerStatusConditionEvent&lt;/strong&gt;](scannerstatusconditionevent.md)"><strong>ScannerStatusConditionEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**DeviceConditionCleared**要素が含まれています、 [ **ConditionId** ](conditionid.md)と[ **ConditionClearTime** ](conditioncleartime.md)要素で、条件の識別子とする条件をオフにしたそれぞれの時刻を指定します。 WSD スキャン サービスの送信、 **DeviceConditionCleared**要素内のクライアントに、 [ **ScannerStatusConditionClearedEvent** ](scannerstatusconditionclearedevent.md)イベント要素。

## <a name="see-also"></a>関連項目


[**ConditionClearTime**](conditioncleartime.md)

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






