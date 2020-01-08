---
title: ScannerStatusConditionEvent 要素
description: 必須の ScannerStatusConditionEvent 要素は、スキャンデバイスの1つのステータス変更に関する詳細情報をクライアントに提供します。
ms.assetid: 0a61fe67-ea1e-4143-afb8-edcdf50ee7c4
keywords:
- ScannerStatusConditionEvent 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2cdfc945ab0b909affd44dc71ab407becbc0da
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653006"
---
# <a name="scannerstatusconditionevent-element"></a>ScannerStatusConditionEvent 要素


必須の**Scannerstatusconditionevent**要素は、スキャンデバイスの1つのステータス変更に関する詳細情報をクライアントに提供します。

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

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、 [**ActiveConditions**](activeconditions.md) element テーブルで[**DeviceCondition**](devicecondition.md)要素が追加または変更されたときに、 **scannerstatusconditionevent**要素をクライアントに送信します。 **Scannerstatusconditionevent**の本体には、new または changed **DeviceCondition**要素が含まれています。

WSD Scan サービスは、報告された**DeviceCondition**がクリアされたときに、 [**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)要素をクライアントに送信する必要があります。

<a name="examples"></a>例
--------

次のコード例は、スキャンデバイスがスキャンランプの障害についてクライアントに通知する方法を示しています。

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionEvent
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

## <a name="see-also"></a>「

[**ActiveConditions**](activeconditions.md)

[**DeviceCondition**](devicecondition.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)
