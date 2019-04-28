---
title: JobEndStateEvent 要素
description: 必要な JobEndStateEvent 要素は、スキャナーのジョブの処理が完了したことをクライアントに通知します。
ms.assetid: 2d5307fb-9c64-413d-8c5c-439012a44a19
keywords:
- JobEndStateEvent 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobEndStateEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a0d74c1976d7dba8bbfbce13b4970a91f2ce309
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377583"
---
# <a name="jobendstateevent-element"></a>JobEndStateEvent 要素


必要な**JobEndStateEvent**要素は、スキャナーのジョブの処理が完了したことをクライアントに通知します。

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

WSD スキャン サービスの送信、 **JobEndStateEvent**スキャナーのジョブの処理が完了すると、クライアントに event 要素。 **JobEndStateEvent**および、完了したジョブの完了に関する詳細を識別するデータ要素が含まれています。

<a name="examples"></a>例
--------

次のコード例では、デバイスのスキャンが最終的な状態のクライアントと 253 のジョブの状態をユーザーに通知方法を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/JobEndStateEvent
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

## <a name="see-also"></a>関連項目


[**JobEndState**](jobendstate.md)

 

 






