---
title: Getjobelement Request 要素
description: 必須の Getjobの要求要素は、JobId 要素によって識別されるジョブに関連する情報を要求します。
ms.assetid: ba8260f4-300f-447e-ad62-d2e4fa2811ef
keywords:
- Getjobの要求要素のイメージ作成デバイス
topic_type:
- apiref
api_name:
- wscn GetJobElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e4f663869f2da91fcfe46d0bba0c1f42854eb9
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652996"
---
# <a name="getjobelementsrequest-element"></a>Getjobelement Request 要素


必須の**Getjobの要求**要素は、 [**JobId**](jobid.md)要素によって識別されるジョブに関連する情報を要求します。

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

WSD Scan サービスは、 **Getjobの要求**操作をサポートする必要があります。

クライアントは、 **Getjobelements 要求**を呼び出して、 [**JobId**](jobid.md)が識別するジョブのジョブ関連の要素の値を決定できます。 WSD Scan サービスは**Getjobの応答**で応答する必要があります。 スキャンサービスが返す情報は、スキーマのスキャンジョブに関連する部分に完全に準拠している必要があります。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

**Getjobの要求**も、次のエラーを返すことがあります。

-   **ClientErrorJobIdNotFound**

    スキャナーが JobId 値に一致するジョブを見つけることができません。または、JobId 値が定義された範囲内にありません。

    | Fault プロパティ | 定義                         |
    |----------------|------------------------------------|
    | \[コード\]       | soap: 送信者                        |
    | \[サブコード\]    | wscn: ClientErrorJobIdNotFound      |
    | \[Reason\]     | 指定された JobId が見つかりませんでした。 |
    | \[詳細\]     | JobId: JobId が正しくありません             |

     

<a name="examples"></a>例
--------

次のコード例では、Fault プロパティ1が識別するスキャンジョブの状態を要求します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
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

## <a name="see-also"></a>「


[**Getjobを応答する**](getjobelementsresponse.md)

[**JobId**](jobid.md)

[**RequestedElements**](requestedelements.md)

 

 






