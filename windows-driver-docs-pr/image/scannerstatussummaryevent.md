---
title: Scantorstatusのイベント要素
description: 必須の Scantorstatusイベント要素は、スキャンデバイスの状態が変更されたことをクライアントに通知します。
ms.assetid: a1297e25-1136-49ef-8b8e-e7c8c62bec13
keywords:
- Scantorstatusのイベント要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatusSummaryEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89df739aaf5cd6b3d5800b0848984f1733444f7f
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653004"
---
# <a name="scannerstatussummaryevent-element"></a>Scantorstatusのイベント要素


必須の**Scantorstatusイベント**要素は、スキャンデバイスの状態が変更されたことをクライアントに通知します。

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

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、スキャンデバイスの状態が変化するたびに、 **Scantorstatusのイベント**要素をクライアントに送信する必要があります。

**Scantorstatussummary イベント**の本文には、スキャナーの状態への変更を説明する[**statussummary**](statussummary.md)要素が含まれている必要があります。

<a name="examples"></a>例
--------

次のコード例は、メディアフィードパスの紙詰まりが原因で、スキャンデバイスが停止したことを示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusSummaryEvent
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

## <a name="see-also"></a>「


[**StatusSummary**](statussummary.md)

 

 






