---
title: JobStatusEvent 要素
description: 必要な JobStatusEvent 要素は、ジョブの状態が変更されたことをクライアントに通知します。
ms.assetid: 8cb510ef-9622-48d0-859d-e52c9b5b8190
keywords:
- JobStatusEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobStatusEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d24694e35bc5ce8863c62f4401a481097df495
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348767"
---
# <a name="jobstatusevent-element"></a>JobStatusEvent 要素


必要な**JobStatusEvent**要素は、クライアントには、ジョブの状態が変更されたことを通知します。

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

WSD スキャン サービスに送信する**JobStatusEvent**ジョブの状態が変更されたときに、クライアントに要素。 **JobStatusEvent**が含まれています、 [ **JobStatus** ](jobstatus.md)すべてのジョブの現在の状態に関する情報を定義する要素。 最初の**JobStatusEvent**メッセージは、通常、 [ **JobId** ](jobid.md)要素と[ **JobState** ](jobstate.md)の**開始**します。

<a name="examples"></a>例
--------

次のコード例では、デバイスのスキャン、253 のジョブの現在の状態に関するクライアントに通知する方法を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/JobStatusEvent
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

## <a name="see-also"></a>関連項目


[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStatus**](jobstatus.md)










