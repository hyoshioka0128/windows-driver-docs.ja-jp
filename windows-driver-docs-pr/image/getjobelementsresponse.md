---
title: GetJobElementsResponse 要素
description: 必要な GetJobElementsResponse 要素は、クライアントが要求するジョブに関連する情報を返します。
ms.assetid: b27c1aba-eb5f-4446-ab34-c03a969e954f
keywords:
- GetJobElementsResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetJobElementsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f702c3e0b8182ca84ff0317de778fd02a22f0c2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529955"
---
# <a name="getjobelementsresponse-element"></a>GetJobElementsResponse 要素


必要な**GetJobElementsResponse**要素は、クライアントを要求するジョブに関連する情報を返します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetJobElementsResponse>
  child elements
</wscn:GetJobElementsResponse>
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
<td><p><a href="jobelements.md" data-raw-source="[&lt;strong&gt;JobElements&lt;/strong&gt;](jobelements.md)"><strong>JobElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetJobElementsResponse**操作。

クライアントが呼び出す**GetJobElementsRequest**ジョブのジョブに関連する要素の値を決定する[ **JobId** ](jobid.md)を識別します。 WSD スキャン サービスの応答でなければなりません、 **GetJobElementsResponse**要求された情報を含む要素。 スキャン サービスが返す情報は、スキーマのスキャン ジョブに関連する部分に完全に準拠する必要があります。

<a name="examples"></a>例
--------

次のコード例では、スキャン サービスは、ジョブ Id 1 を識別するジョブのジョブの状態を返します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobElementsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobElementsResponse>
      <wscn:JobElements>
        <wscn:ElementData wscn:Name="JobStatus" wscn:Valid="true">
          <wscn:JobStatus>
            <wscn:JobId>1</wscn:JobId>
            <wscn:JobState>Completed</wscn:JobState>
            <wscn:JobStateReasons>
              <wscn:JobStateReason>None</wscn:JobStateReason>
            </wscn:JobStateReasons>
            <wscn:ScansCompleted>1</wscn:ScansCompleted>
          </wscn:JobStatus>
        </wscn:ElementData>
      </wscn:JobElements>
    </wscn:GetJobElementsResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**JobElements**](jobelements.md)

[**JobId**](jobid.md)










