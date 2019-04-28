---
title: RetrieveImageResponse 要素
description: RetrieveImageResponse 操作の必要な要素は、クライアントに、スキャン データを返します。
ms.assetid: f63398c4-bbae-42ca-94c5-059b066c65cb
keywords:
- RetrieveImageResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn RetrieveImageResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 225908d15af4b9e1c0e37427e82e8b5d76e8aece
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381584"
---
# <a name="retrieveimageresponse-element"></a>RetrieveImageResponse 要素


必要な**RetrieveImageResponse**操作の要素では、スキャン データをクライアントに返します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:RetrieveImageResponse>
  child elements
</wscn:RetrieveImageResponse>
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
<td><p><a href="scandata.md" data-raw-source="[&lt;strong&gt;ScanData&lt;/strong&gt;](scandata.md)"><strong>ScanData</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **RetrieveImageResponse**操作の要素。 成功したクライアントが送信すると、スキャン サービスがこの要素を送信する[ **RetrieveImageRequest** ](retrieveimagerequest.md)要素。

スキャン サービスでは、スキャン データを返しますでバイナリ添付ファイルとして、 **RetrieveImageResponse**パケット。 応答の MIME マルチパートに関連するコンテンツの種類としてパッケージ化する必要があります、SOAP Message Transmission Optimization Mechanism を使用\[MTOM\]を効率的に画像のバイナリ データを送信します。

結果のファイルのスキャン サービスが返すイメージの数の組み合わせによって異なります、 [ **ImagesToTransfer** ](imagestotransfer.md)の要素、 [ **ScanTicket**](scanticket.md)とイメージ ファイル[**形式**](format.md)要素として次のとおりです。

-   場合**形式**1 つのイメージ形式を指定します、返されるファイルは 1 つのイメージを常に含まれます。
-   場合**形式**複数ページの形式を指定します、返されたファイルが最大の値、入力ソースがスキャンできる多数のイメージが格納されます**ImagesToTransfer**します。

場合[**形式**](format.md) 1 つのイメージ形式との値を指定します[ **ImagesToTransfer** ](imagestotransfer.md) 0 または 1 より大きいは、クライアントが送信されます繰り返し[ **RetrieveImageRequest** ](retrieveimagerequest.md)操作要素で、スキャン サービスが応答するまで、 **ClientErrorNoImagesAvailable**エラーまで、または、**ImagesToTransfer**値が満たされています。

スキャン サービスを使用してジョブを中止する必要があります、 [ **JobStateReason** ](jobstatereason.md)の**ImageTransferError**イメージ データの転送中に通信エラーがある場合。

<a name="examples"></a>例
--------

次のコード例では、WSD スキャン サービスがクライアントにイメージ データを送信する方法を示します。

```xml
mime-version: 1.0
Content-Type: multipart/related;
    type=application/xop+xml;
    boundary=4aa7d814-adc1-47a2-8e1c-07585b9892a4;
    start="<14629f74-2047-436c-8046-5cac76d280fc@uuid>";
    startinfo=application/soap+xml


--4aa7d814-adc1-47a2-8e1c-07585b9892a4
Content-Type: application/xop+xml; type="application/soap+xml"
                                   charset=UTF-8
Content-Transfer-Encoding: binary
Content-ID: <14629f74-2047-436c-8046-5cac76d280fc@uuid>

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="http://www.w3.org/2003/12/xop/include"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheRetrieveImageRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:RetrieveImageResponse>
      <wscn:ScanData>
        <xop:Include href="cid:1c696bd7-005a-48d9-9ee9-9adca11f8892@uuid" />
      </wscn:ScanData>
    </wscn:RetrieveImageResponse>
  </soap:Body>
</soap:Envelope>

--4aa7d814-adc1-47a2-8e1c-07585b9892a4

Content-Type: image/jpeg;
Content-Transfer-Encoding: binary
Content-ID: <1c696bd7-005a-48d9-9ee9-9adca11f8892@uuid >

Binary Scan Data
--4aa7d814-adc1-47a2-8e1c-07585b9892a4--
```

## <a name="see-also"></a>関連項目

[**書式設定**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**JobStateReason**](jobstatereason.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

[**ScanData**](scandata.md)

[**ScanTicket**](scanticket.md)
