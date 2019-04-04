---
title: GetJobElementsRequest 要素
description: 必要な GetJobElementsRequest 要素は、ジョブ Id 要素を識別する、ジョブに関連する情報を要求します。
ms.assetid: ba8260f4-300f-447e-ad62-d2e4fa2811ef
keywords:
- GetJobElementsRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetJobElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c3eb4f27339aeca645f764327371b11d9875b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561117"
---
# <a name="getjobelementsrequest-element"></a>GetJobElementsRequest 要素


必要な**GetJobElementsRequest**要素は、ジョブに関連する情報を要求する、 [ **JobId** ](jobid.md)要素を識別します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetJobElementsRequest>
  child elements
</wscn:GetJobElementsRequest>
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
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetJobElementsRequest**操作。

クライアントが呼び出すことができます**GetJobElementsRequest**ジョブのジョブに関連する要素の値を決定する[ **JobId** ](jobid.md)を識別します。 WSD スキャン サービスの応答でなければなりません、 **GetJobElementsResponse**します。 スキャン サービスが返す情報は、スキーマのスキャン ジョブに関連する部分に完全に準拠する必要があります。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、[WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)を参照してください。

**GetJobElementsRequest**次のエラーを返すも可能性があります。

-   **ClientErrorJobIdNotFound**

    スキャナーは、ジョブ Id 値と一致するジョブを見つけることができませんまたはジョブ Id 値が定義された範囲内です。

    | Fault プロパティ | 定義                         |
    |----------------|------------------------------------|
    | \[コード\]       | soap 送信者:                        |
    | \[サブコード\]    | wscn:ClientErrorJobIdNotFound      |
    | \[理由\]     | 指定したジョブ Id が見つかりませんでした。 |
    | \[詳細\]     | JobId:JobId が正しくありません。             |

     

<a name="examples"></a>例
--------

次のコード例では、Fault プロパティ 1 を識別するスキャン ジョブの状態を要求します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobElements>
      <wscn:JobId>1</wscn:JobId>
      <wscn:RequestedElements>
        <wscn:Name>JobStatus</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetJobElements>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobId**](jobid.md)

[**RequestedElements**](requestedelements.md)

 

 






