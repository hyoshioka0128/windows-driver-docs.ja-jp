---
title: GetJobHistoryResponse 要素
description: 必要な GetJobHistoryResponse 要素は、完了したジョブの概要を返します。
ms.assetid: 85c9edb4-fe6c-49a7-899a-71ce65e38852
keywords:
- GetJobHistoryResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetJobHistoryResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04a3256ed576a77e70ca853278675f3f550791b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346198"
---
# <a name="getjobhistoryresponse-element"></a>GetJobHistoryResponse 要素


必要な**GetJobHistoryResponse**要素が完了したジョブの概要を返します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetJobHistoryResponse>
  child elements
</wscn:GetJobHistoryResponse>
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
<td><p><a href="jobhistory.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetJobHistoryResponse**操作の要素。

クライアントが呼び出すことができます[ **GetJobHistoryRequest** ](getjobhistoryrequest.md)前に完了したジョブのジョブに関連する変数の値を決定します。 WSD スキャン サービスの応答でなければなりません、 **GetJobHistoryResponse**クライアントが要求した情報が含まれる操作の要素または適切なエラー コード。

WSD スキャン サービスを保持するジョブ履歴の量は、実装に固有です。

<a name="examples"></a>例
--------

次のコード例では、ジョブ履歴ジョブ履歴のクライアントの要求に応答が返されない方法を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory />
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

次のコード例では、ジョブと関連付けられているデータの最後の 2 つの完了したジョブの一覧を返します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Completed</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>4</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneRogers</wscn:JobOriginatingUserName>
          <wscn:JobState>Canceled</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobCanceledAtDevice</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>1</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:JobHistory>
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**JobHistory**](jobhistory.md)










