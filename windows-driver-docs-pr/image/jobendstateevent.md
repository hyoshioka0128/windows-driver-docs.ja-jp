---
title: JobEndStateEvent 要素
description: Required JobEndStateEvent 要素は、スキャナーがジョブの処理を完了したことをクライアントに通知します。
ms.assetid: 2d5307fb-9c64-413d-8c5c-439012a44a19
keywords:
- JobEndStateEvent 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn JobEndStateEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74bb42fa3d5533b0a99909eefaf767080d82ad83
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652984"
---
# <a name="jobendstateevent-element"></a>JobEndStateEvent 要素


Required **Jobendstateevent**要素は、スキャナーがジョブの処理を完了したことをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobEndStateEvent>
  child elements
</wscn:JobEndStateEvent>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、スキャナーがジョブの処理を終了したときに、 **Jobendstateevent**イベント要素をクライアントに送信します。 **Jobendstateevent**には、完了したジョブとその完了に関する詳細を識別するデータ要素が含まれています。

<a name="examples"></a>例
--------

次のコード例は、スキャンデバイスが、ジョブ253の最終状態と状態をクライアントに通知する方法を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/JobEndStateEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:JobEndStateEvent>
      <wscn:JobEndState>
        <wscn:JobId>253</wscn:JobId>
        <wscn:JobCompletedState>Completed</wscn:JobCompletedState>
        <wscn:JobCompletedStateReasons>
          <wscn:JobStateReason>JobCompletedWithWarnings</wscn:JobStateReason>
        </wscn:JobCompletedStateReasons>
        <wscn:JobName>Scan from Imaging App</wscn:JobName>
        <wscn:JobOriginatingUserName>User</wscn:JobOriginatingUserName>
        <wscn:ScansCompleted>7</wscn:ScansCompleted>
        <wscn:JobCompletedTime>2006-01-24T11:37:05.673Z</wscn:JobCompletedTime>
      </wscn:JobEndState>
    </wscn:JobEndStateEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>「


[**JobEndState**](jobendstate.md)

 

 






