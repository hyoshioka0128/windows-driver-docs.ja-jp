---
title: GetActiveJobsResponse 要素
description: 必要な GetActiveJobsResponse 要素は、すべてのスキャンが現在アクティブなジョブのジョブに関連する変数の概要を返します。
ms.assetid: 77efef7f-451d-49f8-80c1-6ab12c98ee7b
keywords:
- GetActiveJobsResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetActiveJobsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e42d915720be7b96214a9fc098c53c97e4aaa0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353014"
---
# <a name="getactivejobsresponse-element"></a>GetActiveJobsResponse 要素


必要な**GetActiveJobsResponse**要素が現在アクティブなスキャンのすべてのジョブのジョブに関連する変数の概要を返します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetActiveJobsResponse>
  child elements
</wscn:GetActiveJobsResponse>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetActiveJobsResponse**操作。

クライアントが呼び出すことができます[ **GetActiveJobsRequest** ](getactivejobsrequest.md)現在アクティブなスキャンのすべてのジョブのジョブに関連する変数の値を決定します。 WSD スキャン サービスの応答でなければなりません、 **GetActiveJobsResponse**のよく寄せられるクライアント情報を格納する要素または適切なエラー コード。

**GetActiveJobsResponse**が含まれています、 [ **ActiveJobs** ](activejobs.md)すべてのジョブの概要を含む要素。

<a name="examples"></a>例
--------

次のコード例では、アクティブなスキャン ジョブがないという事実を返す方法を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetActiveJobsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsResponse>
      <wscn:ActiveJobs/>
    </wscn:GetActiveJobsResponse >
  </soap:Body>
</soap:Envelope>
```

次のコード例では、2 つのアクティブなスキャン ジョブを報告します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetActiveJobsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsResponse>
      <wscn:ActiveJobs>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Processing</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobScanning</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>2</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneSmith</wscn:JobOriginatingUserName>
          <wscn:JobState>Pending</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>0</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:ActiveJobs>
    </wscn:GetActiveJobsResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**ActiveJobs**](activejobs.md)

[**GetActiveJobsRequest**](getactivejobsrequest.md)










