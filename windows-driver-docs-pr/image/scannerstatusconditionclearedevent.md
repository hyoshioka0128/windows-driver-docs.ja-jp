---
title: ScannerStatusConditionClearedEvent 要素
description: 必要な ScannerStatusConditionClearedEvent 要素は、スキャナーで以前に報告された DeviceCondition 条件がクリアされたことをクライアントに通知します。
ms.assetid: c849caba-d77b-441b-a5e1-94f9285cef3f
keywords:
- ScannerStatusConditionClearedEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionClearedEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bee70559ed044dd9fd3a566e9d74c222f5daf3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386303"
---
# <a name="scannerstatusconditionclearedevent-element"></a>ScannerStatusConditionClearedEvent 要素


必要な**ScannerStatusConditionClearedEvent**要素をクライアントに通知を以前に報告された[ **DeviceCondition** ](devicecondition.md)条件がクリアされた時刻、スキャナーです。

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

WSD スキャン サービスに送信、 **ScannerStatusConditionClearedEvent**でデバイスが条件をときに要素が識別される[ **ScannerStatusConditionEvent** ](scannerstatusconditionevent.md)されましたオフにします。 **ScannerStatusConditionClearedEvent**が含まれています、 [ **DeviceConditionCleared** ](deviceconditioncleared.md)クリアされた条件とクリアされて時刻を含む要素。

<a name="examples"></a>例
--------

次のコード例では、デバイスが ConditionId 1543 が識別される前の状態がクリアするクライアントをユーザーに通知方法を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionClearedEvent
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

## <a name="see-also"></a>関連項目

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)
