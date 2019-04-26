---
title: ValidateScanTicketResponse 要素
description: 必要な ValidateScanTicketResponse 操作は、ScanTicket が有効では、クライアントが送信されたかどうかをクライアントに通知します。
ms.assetid: 7eea7d33-45de-45bf-8e89-de06f5710073
keywords:
- ValidateScanTicketResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff2009f01a1ad98b1b2ef9d4484094a9fdb91c5b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356184"
---
# <a name="validatescanticketresponse-element"></a>ValidateScanTicketResponse 要素


必要な**ValidateScanTicketResponse**操作は、クライアントの送信になっているかどうかをクライアントに通知[ **ScanTicket** ](scanticket.md)は有効です。

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

クライアントが送信、 [ **ScanTicket** ](scanticket.md)にチェックインする要素、 [ **ValidateScanTicketRequest** ](validatescanticketrequest.md)操作。 WSD スキャン サービスの応答でなければなりません、 **ValidateScanTicketResponse**要素が正常に処理後のすべての検証情報を含む**ValidateScanTicketRequest**します。

<a name="examples"></a>例
--------

次のコード例は、有効なスキャンのチケットを送信したときに、クライアントへの応答を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="http://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="http://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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

次のコード例は、無効なスキャンのチケットを送信したときに、クライアントへの応答を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="http://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="http://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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

## <a name="see-also"></a>関連項目

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidationInfo**](validationinfo.md)
