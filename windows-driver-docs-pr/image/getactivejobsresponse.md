---
title: GetActiveJobsResponse 要素
description: Required GetActiveJobsResponse 要素は、現在アクティブなすべてのスキャンジョブのジョブ関連変数の概要を返します。
ms.assetid: 77efef7f-451d-49f8-80c1-6ab12c98ee7b
keywords:
- GetActiveJobsResponse 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn GetActiveJobsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02e604cc11af151776ea059e2102abc8c0439d1d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652978"
---
# <a name="getactivejobsresponse-element"></a>GetActiveJobsResponse 要素


Required **GetActiveJobsResponse**要素は、現在アクティブなすべてのスキャンジョブのジョブ関連変数の概要を返します。

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

WSD Scan サービスは、 **GetActiveJobsResponse**操作をサポートしている必要があります。

クライアントは、 [**GetActiveJobsRequest**](getactivejobsrequest.md)を呼び出して、現在アクティブなすべてのスキャンジョブのジョブ関連変数の値を確認できます。 WSD Scan サービスは、クライアントが要求した情報または適切なエラーコードを含む**GetActiveJobsResponse**要素で応答する必要があります。

**GetActiveJobsResponse**には、すべてのジョブの概要を含む[**activejobs**](activejobs.md)要素が含まれています。

<a name="examples"></a>例
--------

次のコード例は、アクティブなスキャンジョブがないという事実を返す方法を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
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

次のコード例では、2つのアクティブなスキャンジョブを報告します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
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

## <a name="see-also"></a>「


[**ActiveJobs**](activejobs.md)

[**GetActiveJobsRequest**](getactivejobsrequest.md)










