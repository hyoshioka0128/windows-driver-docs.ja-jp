---
title: DeviceCondition 要素
description: 省略可能な DeviceCondition 要素は、スキャナーの現在アクティブな条件のいずれかの詳細を提供します。
ms.assetid: 5e68462f-afa9-40d4-843a-7d15fb7c98e3
keywords:
- DeviceCondition 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DeviceCondition wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92558cbe7ec9c321fe27a6b19895dbccaf58db86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364556"
---
# <a name="devicecondition-element"></a>DeviceCondition 要素


省略可能な**DeviceCondition**要素は、スキャナーの現在アクティブな条件のいずれかの詳細を提供します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DeviceCondition wscn:Id="..."
  Id = "xs:string">
  child elements
</wscn:DeviceCondition wscn:Id="...">
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
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>id</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
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
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>コンポーネント</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name Elementfor DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>名前 Elementfor DeviceCondition と ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>重要度</strong></a></p></td>
</tr>
<tr class="even">
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
<td><p><a href="activeconditions.md" data-raw-source="[&lt;strong&gt;ActiveConditions&lt;/strong&gt;](activeconditions.md)"><strong>ActiveConditions</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスの一意の識別子を指定します、 **Id**この属性**DeviceCondition**要素。 クライアントが使用できる**Id**の値と共に、 [**時間**](time.md)要素が、エラー状態が新しいかがなくなったかを判断します。 WSD スキャン サービスには、可能な限りの識別子が再利用する必要があります。 この遅延により、クライアントは正確の追跡個々**DeviceCondition**要素。

WSD スキャン サービスでは、スキャナーの状態の変更点について、クライアントを通知を送信して、 [ **ScannerStatusConditionEvent** ](scannerstatusconditionevent.md)イベント。 クライアントは直接呼び出すことによって、スキャナーの状態をクエリ、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

## <a name="see-also"></a>関連項目


[**ActiveConditions**](activeconditions.md)

[**コンポーネント**](component.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**名前 Elementfor DeviceCondition と ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

[**重要度**](severity.md)

[**時間**](time.md)

 

 






