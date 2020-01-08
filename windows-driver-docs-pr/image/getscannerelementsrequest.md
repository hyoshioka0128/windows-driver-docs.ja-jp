---
title: Getscanの要求要素
description: 必須の Getscanの要求要素を使用すると、クライアントはスキャナーに関する情報を要求できます。
ms.assetid: 9b5baed9-0950-4fbd-9e5b-4ad58dedb87e
keywords:
- Getscanを要求要素のイメージ作成デバイス
topic_type:
- apiref
api_name:
- wscn GetScannerElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ec8fe032a4ce2a8501204491e9d11715787b3c
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652970"
---
# <a name="getscannerelementsrequest-element"></a>Getscanの要求要素


必須の**Getscanの要求**要素を使用すると、クライアントはスキャナーに関する情報を要求できます。

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

WSD Scan サービスは、 **Getscanの要求**操作をサポートする必要があります。

クライアントは、 **Getscanの Elements 要求**を呼び出して、スキャンサービスのスキーマの標準およびベンダーによって拡張された要素を検出できます。 クライアントが利用できる情報には、デバイスのルートレベルでアクセスできるスキャナーデータの一部が含まれています。 この情報には、[説明]、[構成]、[状態]、[既定のスキャンチケット]、およびスキャンサービスのすべてのベンダーの拡張機能が含まれます。

スキャンサービスが**Getscanの要求**を正常に処理した場合は、要求された情報と共に[**Getscanの応答**](getscannerelementsresponse.md)操作が返されます。 そうしないと、スキャンサービスから適切なエラーコードが返されます。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

<a name="examples"></a>例
--------

次のコード例では、クライアントは単一の QName 値 (wscn: ScannerDescription) を指定して、スキャナーの説明を照会します。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
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

次のコード例は、クライアントによるスキャナーの状態の要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
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

次のコード例では、クライアントは2つの QName 値を指定しています。 最初の QName は wscn: ScannerConfiguration で、2番目の qname は無効です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  xmlns:ihv="https://www.example.com/extension"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
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

## <a name="see-also"></a>「


[**Getscanでの応答**](getscannerelementsresponse.md)

[**RequestedElements**](requestedelements.md)

 

 






