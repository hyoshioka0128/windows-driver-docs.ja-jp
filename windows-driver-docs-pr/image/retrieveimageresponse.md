---
title: RetrieveImageResponse 要素
description: Required RetrieveImageResponse operation 要素はスキャンデータをクライアントに返します。
ms.assetid: f63398c4-bbae-42ca-94c5-059b066c65cb
keywords:
- RetrieveImageResponse 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn RetrieveImageResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393e5aef3fc9883f8cf196b9e70391de1ef5df29
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652944"
---
# <a name="retrieveimageresponse-element"></a>RetrieveImageResponse 要素


Required **RetrieveImageResponse** operation 要素はスキャンデータをクライアントに返します。

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
<td><p><a href="scandata.md" data-raw-source="[&lt;strong&gt;ScanData&lt;/strong&gt;](scandata.md)"><strong>スキャンデータ</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、 **RetrieveImageResponse** operation 要素をサポートしている必要があります。 クライアントが[**RetrieveImageRequest**](retrieveimagerequest.md)要素を正常に送信すると、スキャンサービスはこの要素を送信します。

スキャンサービスは、スキャンデータを**RetrieveImageResponse**パケットと共にバイナリ添付ファイルとして返します。 応答は、MIME マルチパート関連のコンテンツタイプとしてパッケージ化され、SOAP メッセージ転送の最適化機構を使用して、バイナリイメージデータを効率的に送信するための MTOM\] \[する必要があります。

スキャンサービスが結果ファイルに返すイメージの数は、次のように、 [**Scanticket**](scanticket.md)の[**ImagesToTransfer**](imagestotransfer.md)要素と image file [**Format**](format.md)要素の組み合わせによって異なります。

-   **Format**で1つの画像形式を指定した場合、返されるファイルには常に1つのイメージが含まれます。
-   **Format**がマルチページ形式を指定する場合、返されるファイルには、入力ソースが**ImagesToTransfer**の値までスキャンできるイメージが多数含まれます。

[**Format**](format.md)で1つの画像形式が指定されており、 [**ImagesToTransfer**](imagestotransfer.md)の値が0または1より大きい場合、クライアントは、スキャンサービスが**ClientErrorNoImagesAvailable** Fault で応答するか、 **ImagesToTransfer**値が満たされるまで、繰り返し[**RetrieveImageRequest**](retrieveimagerequest.md) operation 要素を送信します。

スキャンサービスは、イメージデータの転送中に通信エラーが発生した場合に、 [**JobStateReason**](jobstatereason.md)の**imagetransfererror**を使用してジョブを中止する必要があります。

<a name="examples"></a>例
--------

次のコード例は、WSD Scan サービスがイメージデータをクライアントに送信する方法を示しています。

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
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
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

## <a name="see-also"></a>「

[**形式**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**JobStateReason**](jobstatereason.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

[**スキャンデータ**](scandata.md)

[**スキャンチケット**](scanticket.md)
