---
title: ConditionHistoryEntry 要素
description: 必須の ConditionHistoryEntry 要素は、スキャナーの過去の条件のいずれかの詳細を提供します。
ms.assetid: 2a5d52c2-6389-4afe-be6c-4645d62ccda0
keywords:
- ConditionHistoryEntry 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ConditionHistoryEntry wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d270449409f1722108ef2dbce7ab06e0b60f579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572861"
---
# <a name="conditionhistoryentry-element"></a>ConditionHistoryEntry 要素


必要な**ConditionHistoryEntry**要素は、スキャナーの過去の条件のいずれかの詳細を提供します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ConditionHistoryEntry wscn:Id="..."
  Id = "xs:string">
  child elements
</wscn:ConditionHistoryEntry wscn:Id="...">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>型</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>id</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p></p>
<p>必須。 1 ~ 2147483648 整数。</p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="cleartime.md" data-raw-source="[&lt;strong&gt;ClearTime&lt;/strong&gt;](cleartime.md)"><strong>ClearTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>コンポーネント</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name forParents DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>名前 forParents DeviceCondition と ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>重要度</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="time.md" data-raw-source="[&lt;strong&gt;Time&lt;/strong&gt;](time.md)"><strong>時間</strong></a></p></td>
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
<td><p><a href="conditionhistory.md" data-raw-source="[&lt;strong&gt;ConditionHistory&lt;/strong&gt;](conditionhistory.md)"><strong>ConditionHistory</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

WSD スキャン サービスの一意の識別子を指定します、 **Id**この属性**ConditionHistoryEntry**要素。 クライアントが使用できる**Id**の値と共に、 [**時間**](time.md)要素が、エラー状態が新しいかがなくなったかを判断します。 WSD スキャン サービスには、可能な限りの識別子が再利用する必要があります。 この遅延により、クライアントは正確の追跡個々**ConditionHistoryEntry**要素。

許可される値を拡張することはできません**Id**します。

## <a name="see-also"></a>関連項目


[**ClearTime**](cleartime.md)

[**コンポーネント**](component.md)

[**ConditionHistory**](conditionhistory.md)

[**DeviceCondition**](devicecondition.md)

[**名前 forParents DeviceCondition と ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**重要度**](severity.md)

[**時間**](time.md)

 

 






