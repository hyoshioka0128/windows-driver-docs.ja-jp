---
title: GetScannerElementsRequest 要素
description: 必要な GetScannerElementsRequest 要素では、クライアントがスキャナーに関する情報を要求できるようにします。
ms.assetid: 9b5baed9-0950-4fbd-9e5b-4ad58dedb87e
keywords:
- GetScannerElementsRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetScannerElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c6865d6dde3f9981cced1e2e3b9a466010636d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550236"
---
# <a name="getscannerelementsrequest-element"></a>GetScannerElementsRequest 要素


必要な**GetScannerElementsRequest**要素には、クライアントが要求については、スキャナーができるようにします。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetScannerElementsRequest>
  child elements
</wscn:GetScannerElementsRequest>
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
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetScannerElementsRequest**操作。

クライアントが呼び出すことができます**GetScannerElementsRequest**スキャン サービス スキーマの標準およびベンダー拡張要素を検出します。 クライアントに提供される情報には、デバイスのルート レベルでアクセスできるスキャナー データの任意の部分が含まれます。 この情報には、説明、構成、状態、既定のスキャン チケット、およびスキャン サービスへの任意のベンダー拡張機能が含まれています。

スキャン サービスが正常に処理する場合、 **GetScannerElementsRequest**が返されます、 [ **GetScannerElementsResponse** ](getscannerelementsresponse.md)操作に必要な情報。 それ以外の場合、スキャン サービスでは、適切なエラー コードを返す必要があります。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、次を参照してください。 [WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)します。

<a name="examples"></a>例
--------

次のコード例では、クライアントは、スキャナーの説明に対してクエリを実行する 1 つの QName 値 (wscn:ScannerDescription) を指定します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerDescription</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

次のコード例では、スキャナーの状態に対するクライアントの要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerStatus</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

次のコード例では、クライアントは、2 つの QName 値を指定します。 最初の QName が wscn:ScannerConfiguration、および 2 つ目の QName が無効です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  xmlns:ihv="http://www.example.com/extension"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerConfiguration</wscn:Name>
        <wscn:Name>ihv:InvalidRequestEntry</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetScannerElementsResponse**](getscannerelementsresponse.md)

[**RequestedElements**](requestedelements.md)

 

 






