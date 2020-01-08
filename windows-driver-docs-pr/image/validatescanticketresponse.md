---
title: ValidateScanTicketResponse 要素
description: Required ValidateScanTicketResponse 操作は、クライアントが送信した ScanTicket が有効かどうかをクライアントに通知します。
ms.assetid: 7eea7d33-45de-45bf-8e89-de06f5710073
keywords:
- ValidateScanTicketResponse 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5d211fd8faaa260e774bbd810d667cfda2a42f3
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652940"
---
# <a name="validatescanticketresponse-element"></a>ValidateScanTicketResponse 要素


Required **ValidateScanTicketResponse**操作は、クライアントが送信した[**scanticket**](scanticket.md)が有効かどうかをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ValidateScanTicketResponse>
  child elements
</wscn:ValidateScanTicketResponse>
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
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

クライアントは、 [**ValidateScanTicketRequest**](validatescanticketrequest.md)操作でチェックする[**scanticket**](scanticket.md)要素を送信します。 WSD Scan サービスは、 **ValidateScanTicketRequest**を正常に処理した後、すべての検証情報を含む**ValidateScanTicketResponse**要素で応答する必要があります。

<a name="examples"></a>例
--------

次のコード例では、有効なスキャンチケットを送信したときのクライアントへの応答を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="https://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheValidateScanTicketRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketResponse>
      <wscn:ValidationInfo>
        <wscn:ValidTicket>true</wscn:ScanIdentifierValidTicket>
          <wscn:ImageInformation>
          <wscn:MediaFrontImageInfo>
            <wscn:PixelsPerLine>900</wscn:PixelsPerLine>
            <wscn:NumberOfLines>1500</wscn:NumberOfLines>
            <wscn:BytesPerLine>113</wscn:BytesPerLine>
          </wscn:MediaFrontImageInfo>
        </wscn:ImageInformation>
      </wscn:ValidationInfo>
    </wscn:ValidateScanTicketResponse>
  </soap:Body>
</soap:Envelope>
```

次のコード例は、無効なスキャンチケットを送信したときのクライアントへの応答を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="https://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheValidateScanTicketRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketResponse>
      <wscn:ValidationInfo>
        <wscn:ValidTicket>false</wscn:ValidTicket>
        <wscn:ImageInformation>
          <wscn:MediaFrontImageInfo>
            <wscn:PixelsPerLine>0</wscn:PixelsPerLine>
            <wscn:NumberOfLines>0</wscn:NumberOfLines>
            <wscn:BytesPerLine>0</wscn:BytesPerLine>
          </wscn:MediaFrontImageInfo>
        </wscn:ImageInformation>
        <wscn:ValidScanTicket>
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
              <wscn:ScalingWidth>1000</wscn:ScalingWidth>
              <wscn:ScalingHeight>1000</wscn:ScalingHeight>
            </wscn:Scaling>
            <wscn:MediaSides>
              <wscn:MediaFront>
                <wscn:Resolution>
                  <wscn:Width>300</wscn:Width>
                  <wscn:Height>300</wscn:Height>
                </wscn:Resolution>
              </wscn:MediaFront>
            </wscn:MediaSides>
          </wscn:DocumentParameters>
        </wscn:ValidScanTicket>
      </wscn:ValidationInfo>
    </wscn:ValidateScanTicketResponse>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>「

[**スキャンチケット**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidationInfo**](validationinfo.md)
