---
title: ValidateScanTicketRequest 要素
description: 必須の ValidateScanTicketRequest operation 要素を使用すると、クライアントは、今後のスキャン操作の設定が有効かどうかを判断できます。
ms.assetid: 366b0d71-1494-48fa-94f5-1832d7f119a4
keywords:
- ValidateScanTicketRequest 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e8ae7777343f12162de5f37a4d203b99181244c
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652930"
---
# <a name="validatescanticketrequest-element"></a>ValidateScanTicketRequest 要素


必須の**ValidateScanTicketRequest** operation 要素を使用すると、クライアントは、今後のスキャン操作の設定が有効かどうかを判断できます。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ValidateScanTicketRequest>
  child elements
</wscn:ValidateScanTicketRequest>
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
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>スキャンチケット</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

クライアントは、 **ValidateScanTicketRequest**要素を使用して、さまざまな設定の変更と組み合わせを検証できます。

[**Scanticket**](scanticket.md)には、クライアントが今後のスキャン操作で送信する設定がすべて含まれています。 **Scanticket**には、クライアントがスキャナーで上書きする処理要素だけを含めることができます。また、WSD Scan サービスでサポートされているすべての要素を含めることもできます。

WSD Scan サービスが**ValidateScanTicketRequest**を正常に処理した場合は、 [**ValidateScanTicketResponse**](validatescanticketresponse.md)操作でその検証情報が返されます。 そうしないと、スキャンサービスから適切なエラーコードが返されます。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

この操作では、次のエラーコードが返されることもあります。

-   **Clienterror衝突 Tingrequiredparameters**

    MustHonor 属性が true に設定されている2つ以上の DocumentParameters 要素が競合しています。 MustHonor set true に指定されたすべての設定を使用すると、デバイスで競合が発生します。 スキャンサービスはこの競合を解決できないため、ScanTicket は無効と見なされます。

    | Fault プロパティ | 定義                                                                                                                                                     |
    |----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[コード\]       | soap: 送信者                                                                                                                                                    |
    | \[サブコード\]    | wscn: Clienterror衝突 Tingrequiredparameters                                                                                                                  |
    | \[Reason\]     | DocumentParameters 要素内の複数の要素で MustHonor が true に設定されていますが、すべての設定を true に設定すると、スキャナーデバイスで競合が発生します。 |
    | \[詳細\]     | None                                                                                                                                                           |

     

<a name="examples"></a>例
--------

次のコード例は、有効なスキャンチケットの検証要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketRequest>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Photo Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>dib</wscn:Format>
          <wscn:InputSource>Platen</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:InputMediaSize>
              <wscn:Width>3000</wscn:Width>
              <wscn:Height>5000</wscn:Height>
            </wscn:InputMediaSize>
          </wscn:InputSize>
          <wscn:Scaling>
            <wscn:ScalingWidth>125</wscn:ScalingWidth>
            <wscn:ScalingHeight>125</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:ColorProcessing>GrayScale4</wscn:ColorProcessing>
              <wscn:Resolution>
                <wscn:Width>300</wscn:Width>
                <wscn:Height>300</wscn:Height>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:ValidateScanTicketRequest>
  </soap:Body>
  </soap:Envelope>
```

次のコード例は、無効なスキャンチケットの検証要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketRequest>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Photo Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>jfif</wscn:Format>
          <wscn:InputSource>Platen</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
          </wscn:InputSize>
          <wscn:Scaling>
            <wscn:ScalingWidth>1250</wscn:ScalingWidth>
            <wscn:ScalingHeight>1250</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
          <wscn:MediaFront>
          <wscn:Resolution>
            <wscn:Width>350</wscn:Width>
            <wscn:Height>350</wscn:Height>
          </wscn:Resolution>
          <wscn:MediaFront>
          <wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:ValidateScanTicketRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>「

[**スキャンチケット**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)
