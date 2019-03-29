---
title: ScannerStatusConditionEvent element
description: 必要な ScannerStatusConditionEvent 要素には、スキャン デバイスの 1 つの状態変更に関する詳細な情報をクライアントが提供します。
ms.assetid: 0a61fe67-ea1e-4143-afb8-edcdf50ee7c4
keywords:
- ScannerStatusConditionEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f017efb6e15d450f79c169d21ecffde4be19fee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581882"
---
# <a name="scannerstatusconditionevent-element"></a>ScannerStatusConditionEvent element


必要な**ScannerStatusConditionEvent**要素は、クライアント デバイスのスキャンで 1 つの状態の変更に関する詳細を提供します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStatusConditionEvent>
  child elements
</wscn:ScannerStatusConditionEvent>
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
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>コメント
-------

WSD スキャン サービスに送信、 **ScannerStatusConditionEvent**クライアントに要素と、 [ **DeviceCondition** ](devicecondition.md)要素が追加または変更、 [ **ActiveConditions** ](activeconditions.md)要素テーブル。 本文**ScannerStatusConditionEvent**新規または変更が含まれています**DeviceCondition**要素。

WSD スキャン サービスに送信する必要があります、 [ **ScannerStatusConditionClearedEvent** ](scannerstatusconditionclearedevent.md)クライアントに要素と、報告された**DeviceCondition**がクリアされました。

<a name="examples"></a>使用例
--------

次のコード例では、デバイスのスキャンでスキャン lamp エラーについて、クライアントがユーザーに通知方法を示します。

```xml
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusConditionEvent>
      <wscn:DeviceCondition wscn:Id="1543">
        <wscn:Time>2006-01-21T17:22:27.5242689Z</wscn:Time>
        <wscn:Name>LampError</wscn:Name>
        <wscn:Component>Platen</wscn:Component>
        <wscn:Severity>Critical</wscn:Severity>
      </wscn:DeviceCondition>
    </wscn:ScannerStatusConditionEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>関連項目

[**ActiveConditions**](activeconditions.md)

[**DeviceCondition**](devicecondition.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)
