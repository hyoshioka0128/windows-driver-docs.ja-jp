---
title: コンポーネント要素
description: 必要なコンポーネント要素は、現在 DeviceCondition または ConditionHistoryEntry 要素について説明するコンポーネントを識別します。
ms.assetid: 1204d8c6-40a2-4b0b-bf86-a739ae96f54a
keywords:
- コンポーネント要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Component
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08304753deae656990fe1fb629758695a4152a42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373212"
---
# <a name="component-element"></a>コンポーネント要素


必要な**コンポーネント**コンポーネントを識別する要素を現在[ **DeviceCondition** ](devicecondition.md)または[ **ConditionHistoryEntry** ](conditionhistoryentry.md)要素について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Component>
  text
</wscn:Component>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

-   ADF
-   Film
-   MediaPath
-   Platen

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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






