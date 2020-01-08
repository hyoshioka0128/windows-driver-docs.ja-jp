---
title: JobStatusEvent 要素
description: Required JobStatusEvent 要素は、ジョブの状態が変更されたことをクライアントに通知します。
ms.assetid: 8cb510ef-9622-48d0-859d-e52c9b5b8190
keywords:
- JobStatusEvent 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn JobStatusEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ffd91141af72f57158b1a6181706369d28299e
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652982"
---
# <a name="jobstatusevent-element"></a>JobStatusEvent 要素


Required **Jobstatusevent**要素は、ジョブの状態が変更されたことをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobStatusEvent>
  child elements
</wscn:JobStatusEvent>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、ジョブの状態が変化したときに**Jobstatusevent**要素をクライアントに送信します。 **Jobstatusevent**には、ジョブの現在の状態に関するすべての情報を定義する[**JobStatus**](jobstatus.md)要素が含まれています。 最初の**Jobstatusevent**メッセージには、通常、 [**JobId**](jobid.md)要素と、 [**jobstate**](jobstate.md)が**開始**されています。

<a name="examples"></a>例
--------

次のコード例は、スキャンデバイスが、ジョブ253の現在の状態についてクライアントに通知する方法を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/JobStatusEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:JobStatusEvent>
      <wscn:JobStatus>
        <wscn:JobId>253</wscn:JobId>
        <wscn:JobState>Processing</wscn:JobState>
        <wscn:JobStateReasons>
          <wscn:JobStateReason>JobScanning</wscn:JobStateReason>
        </wscn:JobStateReasons>
        <wscn:ScansCompleted>4</wscn:ScansCompleted>
        <wscn:JobCreatedTime>2006-01-24T11:34:35.8345Z</wscn:JobCreatedTime>
      </wscn:JobStatus>
    </wscn:JobStatusEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>「


[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStatus**](jobstatus.md)










