---
title: Getjobを Response 要素
description: 必須の Getjobrequests Response 要素は、クライアントが要求するジョブ関連の情報を返します。
ms.assetid: b27c1aba-eb5f-4446-ab34-c03a969e954f
keywords:
- Getjobelement Response 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn GetJobElementsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db1cd742c000d209ad6f82f86d389970e01d44a
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652976"
---
# <a name="getjobelementsresponse-element"></a>Getjobを Response 要素


必須の**Getjobrequests response**要素は、クライアントが要求するジョブ関連の情報を返します。

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

WSD スキャンサービスは、 **Getjobの応答**操作をサポートする必要があります。

クライアントは、 **Getjobelements 要求**を呼び出して、 [**JobId**](jobid.md)が識別するジョブのジョブ関連の要素の値を決定します。 WSD Scan サービスは、要求された情報を含む**Getjobの response**要素を使用して応答する必要があります。 スキャンサービスが返す情報は、スキーマのスキャンジョブに関連する部分に完全に準拠している必要があります。

<a name="examples"></a>例
--------

次のコード例では、スキャンサービスは、JobId 1 が識別するジョブのジョブの状態を返します。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
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

## <a name="see-also"></a>「


[**Getjobの要求**](getjobelementsrequest.md)

[**JobElements**](jobelements.md)

[**JobId**](jobid.md)










