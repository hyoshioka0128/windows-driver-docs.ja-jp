---
title: ScannerStatusSummaryEvent 要素
description: 必要な ScannerStatusSummaryEvent 要素は、スキャン デバイスの状態が変更されたことをクライアントに通知します。
ms.assetid: a1297e25-1136-49ef-8b8e-e7c8c62bec13
keywords:
- ScannerStatusSummaryEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusSummaryEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc4a96a329fa4ced7e8ab9c4b33b69742d802d43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580064"
---
# <a name="scannerstatussummaryevent-element"></a>ScannerStatusSummaryEvent 要素


必要な**ScannerStatusSummaryEvent**要素は、クライアントにスキャン デバイスの状態が変更されたことを通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStatusSummaryEvent>
  child elements
</wscn:ScannerStatusSummaryEvent>
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
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>コメント
-------

WSD スキャン サービスに送信する必要があります、 **ScannerStatusSummaryEvent**スキャン デバイスの状態が変更されるたびに、クライアントに要素。

本文**ScannerStatusSummaryEvent**含める必要があります、 [ **StatusSummary** ](statussummary.md)スキャナーの状態の変更について説明する要素。

<a name="examples"></a>使用例
--------

次のコード例では、メディアのパスをフィードで紙詰まりのために、デバイスのスキャンが停止していることを示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusSummaryEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusSummaryEvent>
      <wscn:StatusSummary>
        <wscn:ScannerState>Stopped</wscn:ScannerState>
        <wscn:ScannerStateReasons>
          <wscn:ScannerStateReason>MediaJam</wscn:ScannerStateReason>
        </wscn:ScannerStateReasons>
      </wscn:StatusSummary>
    </wscn:ScannerStatusSummaryEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**StatusSummary**](statussummary.md)

 

 






