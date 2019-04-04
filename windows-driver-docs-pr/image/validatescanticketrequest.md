---
title: ValidateScanTicketRequest 要素
description: ValidateScanTicketRequest 操作の必要な要素では、クライアントが今後スキャン操作の設定が有効なかどうかを判断できるようにします。
ms.assetid: 366b0d71-1494-48fa-94f5-1832d7f119a4
keywords:
- ValidateScanTicketRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dda1f11b6123105b0f2c5abfce44704d3d3fd38b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559606"
---
# <a name="validatescanticketrequest-element"></a>ValidateScanTicketRequest 要素


必要な**ValidateScanTicketRequest**操作の要素をクライアントが判別の将来のスキャン操作の設定が有効なかどうかは有効にします。

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
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

クライアントが使用できる、 **ValidateScanTicketRequest**さまざまな設定の変更との組み合わせを検証する要素。

[**ScanTicket** ](scanticket.md)すべてのクライアントが、将来のスキャン操作で送信しようとしています。 設定が含まれています。 **ScanTicket**処理要素であること、クライアントが、スキャナーで、オーバーライドしようとしています。 または、WSD スキャン サービスでサポートされているすべての可能な要素を含めることができますのみを含めることができます。

WSD スキャン サービスが正常に処理する場合、 **ValidateScanTicketRequest**でその検証情報が返されます、 [ **ValidateScanTicketResponse** ](validatescanticketresponse.md)操作。 それ以外の場合、スキャン サービスでは、適切なエラー コードを返す必要があります。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、[WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)を参照してください。

この操作は、次のエラー コードを返すも可能性があります。

-   **ClientErrorConflictingRequiredParameters**

    競合がある 2 つ以上の DocumentParameters 間、MustHonor がある要素属性が設定を true にします。 MustHonor を true に設定されている設定のすべてを使用して、デバイスで競合が発生します。 スキャン サービス、ScanTicket は無効と見なされるために、この競合を解決できません。

    | Fault プロパティ | 定義                                                                                                                                                     |
    |----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[コード\]       | soap 送信者:                                                                                                                                                    |
    | \[サブコード\]    | wscn:ClientErrorConflictingRequiredParameters                                                                                                                  |
    | \[理由\]     | DocumentParameters 要素で複数の要素がある MustHonor true に設定するが、すべての設定を適用する設定を true 競合スキャナーのデバイスで。 |
    | \[詳細\]     | なし                                                                                                                                                           |

     

<a name="examples"></a>例
--------

次のコード例では、有効なスキャンのチケットの検証要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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

次のコード例では、無効なスキャン チケットの検証要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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

## <a name="see-also"></a>関連項目

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)
