---
title: ScannerStatusConditionClearedEvent 要素
description: 必須の ScannerStatusConditionClearedEvent 要素は、以前に報告された DeviceCondition 条件がスキャナーでクリアされたことをクライアントに通知します。
ms.assetid: c849caba-d77b-441b-a5e1-94f9285cef3f
keywords:
- ScannerStatusConditionClearedEvent 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionClearedEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e2d28c03d35c8f81c245dc1a8fbe584fec0cc7
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653010"
---
# <a name="scannerstatusconditionclearedevent-element"></a>ScannerStatusConditionClearedEvent 要素


必須の**ScannerStatusConditionClearedEvent**要素は、以前に報告された[**DeviceCondition**](devicecondition.md)条件がスキャナーでクリアされたことをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStatusConditionClearedEvent>
  child elements
</wscn:ScannerStatusConditionClearedEvent>
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
<td><p><a href="deviceconditioncleared.md" data-raw-source="[&lt;strong&gt;DeviceConditionCleared&lt;/strong&gt;](deviceconditioncleared.md)"><strong>DeviceConditionCleared</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

[**ScanScannerStatusConditionClearedEvent Statusconditionevent**](scannerstatusconditionevent.md)で特定されたデバイスの状態がクリアされた場合、WSD Scan サービスは、要素を送信します。 **ScannerStatusConditionClearedEvent**には、クリアされた条件とそれがクリアされた時刻を含む[**DeviceConditionCleared**](deviceconditioncleared.md)要素が含まれています。

<a name="examples"></a>例
--------

次のコード例は、ConditionId 1543 が識別された以前の状態がクリアされたことをクライアントに通知する方法を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionClearedEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusConditionClearedEvent>
      <wscn:DeviceConditionCleared>
        <wscn:ConditionId>1543</wscn:ConditionId>
        <wscn:ConditionClearTime>
          2006-01-21T17:22:35.8345Z
        </wscn:ConditionClearTime>
      </wscn:DeviceConditionCleared>
    </wscn:ScannerStatusConditionClearedEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>「

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)
